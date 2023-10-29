Carpeta llamada Compratido de Grupos, dentro de aqui, crear el grupo ESO1 (incluir alumno eso1) y ESO2 (crear alumno eso2). Creamos grupos teachers y students tambien

students: eso1. s1
student: eso, s2
students: s3 (alumno3)

teachers solo tiene permiso de lectura, t1 será el que tenga permiso de lectura y escritura, por lo tanto, t2 sólo tendrá permiso de lectura y no de escritura

en grupo students, los teachers tendran escritura y lectura, y los students sólo lectura

en el grupo eso 1, los teachers tendrán lectura y escritua, y el alumno eso1 sólo lectura


en el grupo eso 2, los teachers tendrán lectura y escritua, y el alumno eso2 sólo lectura

por última comprobar si todo está correcto

verificar alumno eso1 no puede leer grupo eso2

verificar: creo una subcarpeta (por ejemplo: matemáticas) en eso1 y que tenga los permisos por defecto 

verificar: teacher 2 no puede escribir en la carpeta teachers


## Práctica 3 "Permisos de seguridad"

### Introducción

En esta práctica crearemos varias carpetas/grupos con sus respectivos usuarios y modificaremos sus permisos

### Desarrollo 

Una vez creada la carpeta grupo_compartido y los respectivos grupos y usuarios, asignamos los permisos a los grupos:
```bash
chmod 755 Compartido de Grupos
chmod 644 Compartido de Grupos/ESO1
chmod 644 Compartido de Grupos/ESO2
chmod 644 Compartido de Grupos/Students
chmod 644 Compartido de Grupos/Teachers
```

## Comprobación de los permisos

Para comprobar que los permisos se han asignado correctamente, podemos utilizar el comando ls -l:
```bash
ls -l Compartido de Grupos
ls -l Compartido de Grupos/ESO1
ls -l Compartido de Grupos/ESO2
ls -l Compartido de Grupos/Students
ls -l Compartido de Grupos/Teachers
```

Para comprobar que el alumno eso1 no puede leer el grupo ESO2, intentaremos acceder a la carpeta grupo_compartido/ESO2 como usuario eso1:
```bash
su eso1
cd grupo_compartido/ESO2
```
En este caso, no tendremos permiso de acceder a la carpeta (lectura)

---

Para comprobar que la subcarpeta matemáticas en el grupo ESO1 tiene los permisos por defecto, podemos utilizar el comando ls -l grupo_compartido/ESO1/matemáticas:
```bash
ls -l Compartido de Grupos/ESO1/matemáticas
```
Deberíamos visualizar algo como:
```bash
drwxr-xr-x 2 eso1 users 4096 Oct 29 18:33 matemáticas
```

Para comprobar que teacher2 no puede escribir en la carpeta Teachers, creamos un archivo en la carpeta como usuario teacher2:
```bash
su teacher2
touch grupo_compartido/Teachers/prueba.txt
```
Así pues, no debería dejarnos crear el archivo, ya que no tenemos permisos de escritura




