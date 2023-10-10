# Logs Centralizados

## Introducción

Los logs son registros que se generan en el sistema informático con el objetivo de monitorizar en detalle los eventos que están sucediendo. Así, si hay algún problema en el sistema o en alguna aplicación, podremos deducir o saber cual es la causa de dicho problema. 

En cuanto a los logs centralizados, es un concepto que hace referencia a la unión de estos registros provenientes de varios sistemas y que son analizados por un sólo servidor centralizado, siendo más eficiente.

## Desarrollo

 Requisitos previos:

Tener(configurar) una máquina cliente
Tener(configurar) una máquina servidor
Instalar el servicio rsyslog
“sudo apt-get install” rsyslog (Para Ubuntu)
“sudo yum install” rsyslog (Para CentOS)


Configuración del cliente

Accedemos al archivo de configuración /etc/rsyslog y lo editamos:

	“sudo vi /etc/rsyslog”



Configuración del servidor

Editamos el archivo de configuración /etc/rsyslog

“sudo vi /etc/rsyslog”

Descomentamos las líneas:

"#Provides UDP syslog reception
$ModLoad imudp
$UDPServerRun 514"

#Provides TCP syslog reception
$ModLoad imtcp
$InputTCPServerRun 514


Configuramos el puerto 514 de manera que el servidor quede habilitado:

sudo ufw allow 514/tcp
sudo ufw allow 514/udp


Reiniciamos el sistema para guardar la configuración

	systemctl restart rsyslog.service
