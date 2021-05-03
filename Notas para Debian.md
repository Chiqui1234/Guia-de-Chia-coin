# Errores comúnes
## Root no tiene acceso al path
Esto sucede al convertirse en root desde un usuario común vía el comando **su**, y origina errores relacionados a dpkg, ldconfig y cualquier otro programa que resida en:
* /sbin
* /usr/sbin
* /usr/local/sbin

Tomando de base el archivo */etc/profile*:
```bash
if [ "`id -u`" -eq 0 ]; then
  PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
else
  PATH="/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games"
fi
export PATH
```
Se debe agregar:

> :/sbin:/usr/sbin:/usr/local/sbin

Dentro de las comillas del primer *PATH*.

Cerrar la sesión, probar de nuevo ¡y voilá!

### Por si no se entendió...

Esa porción de código debería quedarte así:

```bash
if [ "`id -u`" -eq 0 ]; then
  PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/sbin:/usr/sbin:/usr/local/sbin"
else
  PATH="/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games"
fi
export PATH
```
