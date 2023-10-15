## Práctica 2 "Política de contraseñas"

### Introducción

La seguridad de nuestro sistema puede verse amenazada si no disponemos de una configuración apropiada. El objetivo de esta práctica es entender y configurar sus directrices con el fin de obtener un sistema más seguro.

Para ello, utilizaremos el módulo *pam pw_password*, a través del cual podremos modificar las políticas de contraseña.

### Desarrollo

1. **Instalación**
  
  En primer lugar. deberemos instalar el módulo *libpwquality*, a través del cual podremos editar el fichero de configuración "/etc/security/pwquality.conf"

```bash
sudo apt install -y libpam-cracklib libpam-pwquality libpwquality-tools
```

2. **Configuación**

  Editamos el fichero /etc/security/pwquality.conf para modificar nuestra política de contraseña, de manera que la seguridad de nuestro sistema se vea reforzada.

```bash
# La nueva contraseña debe tener 2 nuevos caracteres versus la anterior
difok = 2
# La contraseña deberá tener por lo menos 8 caracteres de longitud
minlen = 8
# Require por lo menos un dígito
dcredit = -1
# Requiere al menos 1 letra mayúscula
ucredit = -1
# Requiere al menos 1 letra minúscula
lcredit = -1
# Requiere al menos 1 carácater especial (no alfanumérico)
ocredit = -1
# Requiere un carácter de cada clase (mayúsculas, minúsculas, digito y otro)
minclass = 4
```
  

3. **Verificación**

Si se han seguido los pasos previos y configurado el fichero anterior con las mismas características, mediante el comando *pwscore* deberíamos poder cambiar la contraseña y comprobar si la configuración se ha aplicado correctamente. Por ejemplo:

```bash
echo prueba | pwscore
```
En este caso, no nos permitirá el cambio de contraseña, ya que incumple con los requisitos necesarios:
- No tiene mínimo 8 caracteres de longitud
- No tiene ningún dígito
- Falta letra mayúscula
- Falta caracter especial

