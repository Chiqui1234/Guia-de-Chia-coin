# Compartir archivos en red

Con el objetivo de tener plots en una máquina que se use como NAS, debemos instalar **Samba** para poder compartir las carpetas dónde se alojan los plots creados.
En mi sistema basado en Debian, hice:

> sudo apt-get install samba smbfs

Una vez que tengas Samba (si te pregunta en tener compatibilidad con *WINS*, le das "Si" u "Ok"), deberás editar el archivo de configuración, dónde se especifica el grupo de trabajo, las carpetas a compartir, etc.

> sudo nano /etc/samba/smb.conf

## Cambiar el grupo de trabajo

Buscá esta línea:

```bash
workgroup = WORKGROUP
```

Indica tu grupo de trabajo. En muchos casos es WORKGROUP (tanto para Windows como Linux), pero en mi caso es TOWERPC, así que voy a borrar **WORKGROUP**  para escribir **TOWERPC**.

## Compartir carpetas

Deberías encontrarte con una línea similar a esta:

```bash
#======================= Share Definitions =======================
```

debajo, todas las carpetas que tiene acceso *Samba*, pero ojo, no todas pueden leerse por un usuario *guest*/*anónimo*, y eso lo sabemos gracias a la propiedad **guest ok**, **browsable**, etc.

Te dejo una plantilla y algunos comentarios default, para que sepas como compartir tu propia carpeta:

```bash
# Entre corchetes [] va el nombre de la carpeta, tal cuál se mostrará al entrar desde un Explorador de archivos a nuestra PC dónde instalamos Samba
[Plots]
path=/home/pc-florida3/chia-final
browseable = yes
read only = yes
guest ok = yes # Esto permite que te puedas loguear como "anónimo" 
# File creation mask is set to 0700 for security reasons. If you want to
# create files with group=rw permissions, set next parameter to 0775.
create mask = 0700
# Directory creation mask is set to 0700 for security reasons. If you want to
# create dirs. with group=rw permissions, set next parameter to 0775.
directory mask = 0700

# By default, \\server\username shares can be connected to by anyone
# with access to the samba server.
# The following parameter makes sure that only "username" can connect
# to \\server\username
# This might need tweaking when using external authentication schemes
# valid users = %S
```

Recordá que podés crear un usuario, ejemplo, **pepe**; para poder acceder a ciertas carpetas desde ese usuario en particular.

## Reiniciar Samba para aplicar cambios

> sudo service smbd restart

