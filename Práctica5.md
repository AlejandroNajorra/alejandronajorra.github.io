## Introducción 
Internet es un canal no seguro, “cualquier” persona podría obtener nuestros datos, para evitar que eso suceda, ciertas informaciones con comunicación confidencial deberían ser cifradas.


## Desarrollo

En esta práctica generaremos un certificado autofirmado que instalaremos en el servidor web (Apache)

### Requisitos previos

Antes que nada, necesitaremos instalar el servidor apache en nuestra máquina virtual:
```bash
sudo apt update
```
```bash
sudo apt upgrade
```
```bash
sudo apt install apache2
```

Podremos comprobar si el apache está activo con el siguiente comando:
```bash
systemctl status apache2.service
```

Seguidamente, instalaremos la herramienta *easy-rsa*, la cual nos permitirá generar una clave privada y el certificado de root público, con el que firmaremos las solicitudes de los clientes y servidores que quieran utilizar nuestro servidor (entidad certidicadora (CA)).
```bash
sudo apt install easy-rsa
```
A partir de aquí, ya podemos proceder a crear nuestra infraestructura de clave pública y entidad certificadora

---

### 1. Infraestructura de clave pública

Desde el directorio de inicio y **sin utilizar** *root* creamos el directorio *easy-rsa*
```bash
mkdir ~/easy-rsa
```

Una vez instalado, crearemos los enlaces simbólicos que irán dirigidos a los archivos del paquete *easy-rsa* instalado anteriormente. Utilizaremos el comando "ln -s"
```bash
ln -s /usr/share/easy-rsa/* ~/easy-rsa/
```
Ya solo nos queda iniciar la clave pública o PKI:
```bash
$cd ~/easy-rsa
$./easyrsa init-pki
```
Nos debería aparecer algo como:
```bash
Output
init-pki complete; you may now create a CA or requests.
Your newly created PKI dir is: /home/sammy/easy-rsa/pki
```

### 3. Entidad de certificación y clave privada

Accedemos al directorio *~/easy-rsa* y creamos y editamos el archivo vars de la siguiente manera:
```bash
~/easy-rsa/vars
set_var EASYRSA_REQ_COUNTRY    "ES"
set_var EASYRSA_REQ_PROVINCE   "Valencia"
set_var EASYRSA_REQ_CITY       "Valencia"
set_var EASYRSA_REQ_ORG        "Valencia"
set_var EASYRSA_REQ_EMAIL      "ejemplo@gmail.com"
set_var EASYRSA_REQ_OU         "Valencia"
set_var EASYRSA_ALGO           "Valencia"
set_var EASYRSA_DIGEST         "1234"
```
Obviamente esto son valores adaptados a la configuración que yo quiero, lo importante es no dejar estos valores en blanco o nos lo completará por defecto.

Guardamos el archivo y activamos la PKI pero esta vez con la opción *build-ca*, para crear nuestro certificado público y el par de claves privadas para nuestra CA

```bash
./easy-rsa build-ca
```
Nos pedirán una contraseña y nombre común 
Output
. . .
Enter New CA Key Passphrase:
Re-Enter New CA Key Passphrase:
. . .
Common Name (eg: your user, host, or server name) [Easy-RSA CA]:

CA creation complete and you may now import and sign cert requests.
Your new CA certificate file for publishing is at:
/home/student/easy-rsa/pki/ca.crt
```


 /home/student/easy-rsa/pki/issued/student-server.crt
(privada): /home/student/practice-csr: student-server.key

## Comprobación

