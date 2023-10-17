## Introducción

La redundancia aporta un nivel más de seguridad en caso de pérdida de datos. Esta práctica la llevaremos a cabo implementando un raid 10 que gestionaremos con volúmenes lógicos


## Desarrollo

**Requisitos previos**

Tener instalado la herramienta *mdadm*
```bash
sudo apt-get install mdadm
```
**Instalación del RAID 10**

En primer lugar, creamos y añadiremos 5 unidades de almacenamiento del mismo tamaño, en nuestro caso de 2GB cada uno, de los cuales 4 serán activos y uno lo tendremos de respuesto, para que en el momento en el que falle cualquiera de las unidades, ésta la reemplace. 

Una vez añadidas, procedemos a crear el array de RAID 10 mediante mdadm


crear raid
luego crear la estructura de volúmenes lógicos, mejora gestión del espacio y escalabilidad



creamos el LVM volumen lógico y físico, lo mostramos con los comandos lvscan,etc. por motivos académicos voy a redimensionar
crear volumen lógico que ocupará un 95%

redimensionar un segundo volumen lógico que ocupe 60 y 40
se mapena al sistema operativo en la carpeta /data001



## Comprobación

crear contenido en el raid, si el raid es de 2GB en total son 4GB; y eliminamos unos de los discos

creamos contenido con el DD, creamos el checksum, quitamos un disco duro, comprobamos que ha sido reemplazado y que no se haya corrompido
