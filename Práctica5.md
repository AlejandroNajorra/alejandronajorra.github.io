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

1. Infraestructura de clave pública

Desde el directorio de inicio y **sin utilizar** *root* creamos el directorio *easy-rsa*
```bash
mkdir ~/easy-rsa
```


2. 


 /home/student/easy-rsa/pki/issued/student-server.crt
(privada): /home/student/practice-csr: student-server.key

## Comprobación

