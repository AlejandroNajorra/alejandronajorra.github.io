## Introducción

La redundancia aporta un nivel más de seguridad en caso de pérdida de datos. Esta práctica la llevaremos a cabo implementando un raid 10 que gestionaremos con volúmenes lógicos


## Desarrollo

**Requisitos previos**

Tener instalado la herramienta *mdadm*
```bash
sudo apt-get install mdadm
```
**Instalación del RAID 10**

En nuesta máquina virtual creamos y añadiremos 5 unidades de almacenamiento del mismo tamaño, en nuestro caso de 2GB cada uno, de los cuales 4 serán activos y uno lo tendremos de respuesto, para que en el momento en el que falle cualquiera de las unidades, ésta la reemplace. 

1. Procedemos a crear el array de RAID 10 mediante mdadm:
```bash
mdadm  --create /dev/md1 --level=raid10 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde
```

2. Una vez creado el RAID 10, añadimos la unidad de repuesto:

```bash
mdadm --add /dev/md1 /dev/sdf
```

3. Guardamos la información del array que acabamos de crear en el archivo /etc/mdadm.conf

```bash
mdadm --detail --scan >> /etc/mdadm.conf
```

4. Editamos el archo /etc/mdadm.conf y borramos las líneas que se repitan para que no haya complicaciones a la hora de iniciar el sistema
```bash
sudo -i
```
```bash
vi /etc/mdadm.conf
```

5. A partir de este momento, podemos crear la estructura de volúmenes lógicos para mejorar la gestión del espacio y la escalabilidad.





creamos el LVM volumen lógico y físico, lo mostramos con los comandos lvscan,etc. por motivos académicos voy a redimensionar
crear volumen lógico que ocupará un 95%

redimensionar un segundo volumen lógico que ocupe 60 y 40
se mapena al sistema operativo en la carpeta /data001



## Comprobación

crear contenido en el raid, si el raid es de 2GB en total son 4GB; y eliminamos unos de los discos

creamos contenido con el DD, creamos el checksum, quitamos un disco duro, comprobamos que ha sido reemplazado y que no se haya corrompido
