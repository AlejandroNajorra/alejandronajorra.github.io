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
```bash
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

Ahora que ya tenemos una entidad certificadora, comprobaremos su funcionamiento generando una clave privada y una solicitud de certificado que firmaremos.

En nuestro caso, lo haremos en un cliente de prueba, un Lubuntu.

### Desarrollo 

1. Instalar el paquete openssl
```bash
sudo apt update
sudo apt install openssl
```
2. Generamos la clave privada

```bash
openssl genrsa -out student-server.key
```
3. Solicitamos un certificado (CSR)

```bash
openssl rew -new -key student-server.key -out student-server.req
```
Rellenamos el certificado
```bash
Output
. . .
-----
Country Name (2 letter code) [XX]: ES
State or Province Name (full name) []: Valencia
Locality Name (eg, city) [Default City]:Valencia
Organization Name (eg, company) [Default Company Ltd]: alejandro
Organizational Unit Name (eg, section) []: alejandro
Common Name (eg, your name or your server's hostname) []:student-server
Email Address []: anajorratuazon@gmail.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

4. Firmar el certificado

En nuestro servidor, la cual hace de entidad certificadora y a través de la herramiento *easy-rsa* firmamos la solicitud de certificado
```bash
cd ~/easy-rsa
./easyrsa import-req /home/student/practice-csr/student-server.req server-alejandro
```
```bash
Output
. . .
The request has been successfully imported with a short name of: server-alejandro
You may now use this name to perform signing operations on this request.
```
Firmamos
```bash
./easyrsa sign-req server server-alejandro
```
5. Obtener el certificado en nuestro cliente con navegador
```bash
scp student@192.168.1.1:/home/student/easy-rsa/pki/issued/server-alejandro.crt /home/alejandron/Downloads
```
Una vez obtenido el certificado en nuestro cliente, iremos a los ajustes de nuestro navegador e importaremos el certificado firmado por nosotros. el cual se encontrará en la carpeta donde habíamos específicado que se enviará, en nuestro caso, la carpeta "Downloads".
