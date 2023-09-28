## Práctica 2 "Política de contraseñas"

### Introducción

La seguridad de nuestro sistema puede verse amenazada si no disponemos de una configuración apropiada. Así pues, el objetivo de esta práctica es entender y configurar sus directrices con el fin de obtener un sistema más seguro.

Para ello, utilizaremos el módulo *pam pw_password*, a través del cual podremos modificar las políticas de contraseña

### Desarrollo

1. **Instalación**
  
  En primer lugar. deberemos instalar el módulo *libpwquality*, a través del cual podremos editar el fichero de configuración "/etc/security/pwquality.conf"

```bash
sudo apt install -y libpam-cracklib libpam-pwquality libpwquality-tools
```

1. **Configuación**

   * Editamos el fichero /etc/security/pwquality.conf
  

2. **Verificación**


### Comprobación

poner 2 ejemplos 

pwscore (debería fallar si no cumple con alguno de las políticas de contraseña)