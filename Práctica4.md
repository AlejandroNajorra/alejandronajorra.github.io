## Introducción

La redundancia aporta un nivel más de seguridad en caso de pérdida de datos. Esta práctica la llevaremos a cabo implementando un raid 10 que gestionaremos con volúmenes lógicos


## Desarrollo

crear raid
luego crear la estructura de volúmenes lógicos, mejora gestión del espacio y escalabilidad








creamos el LVM volumen lógico y físico, lo mostramos con los comandos lvscan,etc. por motivos académicos voy a redimensionar
crear volumen lógico que ocupará un 95%

crear un segundo volumen lógio que ocupe 60 y 40
se mapena al sistema operativo en la carpeta /data001


## Comprobación

crear contenido en el raid, si el raid es de 2GB en total son 4GB; y eliminamos unos de los discos

creamos contenido con el DD, creamos el checksum, quitamos un disco duro, comprobamos que ha sido reemplazado y que no se haya corrompido
