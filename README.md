# Guía de Chia coin (Linux)

Para instalar Chia (usable desde CLI) seguir [este tutorial](https://github.com/Chia-Network/chia-blockchain/wiki/INSTALL).

## Iniciar una cuenta nueva
Una vez que instalás Chia en tu sistema operativo, ejecutá el comando

> chia init

Para recibir una nueva cuenta. En caso de que no te muestre tus claves privadas y/o la frase mnemónica, este comando lo hará:

> chia keys show --show-mnemonic-seed

Guardá todo el output generado por el comando anterior (tales cómo master public y private key, farmer public key, pool public key, Mnemonic seed, etc) en algún lugar seguro. Por ejemplo, yo copio y pego ese contenido en un archivo de texto y luego lo comprimo en formato 7z, encriptado con contraseña.

## Uso de estas keys
* Master public key: es una clave pública que podés compartir con cualquier persona y permite ver tu billetera en modo sólo lectura, es decir, quién tenga esta clave **no** puede transferir tu dinero a otro lado, administrar los plots, etc.
* Farmer public key: es una clave pública para que otros dispositivos puedan generar plots compatibles con tu cuenta Chia, y así poder plotear en simultáneo en varias máquinas para luego tener una PC que use esos plots para minar.
* Pool public key: esta clave pública trabaja en conjunto con *Farmer public key*.
* Mnemonic seed: son 24 palabras que se usan para restaurar completamente tu cuenta Chia (modo lectura/escritura, dando todos los permisos para administrar tus fondos y plots).

## Generar plots compatibles con una cuenta Chia
Abrí una ventana de Powershell (Windows) o terminal (Linux/Mac) y escribí el siguiente comando, habiendo ejecutado **chia plots create -h** antes para saber de qué se trata:

> chia plots create -k 32 -b 3390 -u 128 -r 2 -t /ruta/temporal -d /ruta/final -n 1 -f 99305144715663545df075d33322b313177fb41921746bbada3637912f6316ffbe3082bf1239f28d4eb8db80112b17f7 -p 82ae156f6c292e838da7324ed8f111ce904e66fed3478f3caa21a00113356e3ef7009d69d46c4e5348ef7d66ebaf23f5

----------------------------------------------------------------------------------
### NOTA 1 PARA WINDOWS

En Powershell es probable que tengas que anteponer **./**, antes de escribir "chia" y/o **.exe** después. También deberías añadir la carpeta raíz dónde está chia.exe a las *Variables de entorno* > **PATH**. Busca un tutorial de como agregar programas al PATH si no sabés como.

----------------------------------------------------------------------------------

----------------------------------------------------------------------------------
### NOTA 1 PARA LINUX

En Linux debés ir a la carpeta dónde instalaste Chia y correr:

> . ./activate

Antes de ejecutar el comando que crea los plots.

----------------------------------------------------------------------------------

## Entender los parámetros enviados a Chia
**plots create** es la llamada a una función interna de la wallet Chia, que se encarga de crear plots. Los parámetros *-k*, *-b*, *-u* y *-r* te recomiendo no tocarlos a pesar de que tengas una PC "ploteadora" muy potente. Añadir más threads de procesamiento (aumentando el valor que le sigue a *-r* no aumentó la velocidad al crear plots. De hecho, más de 4 threads lo empeora.
Para saber en detalle qué hacen los parámetros *-t*, *-d*, *-n*, *-f* y *-p*, escribí el comando **chia plots create -h**, pero el valor que le sigue a la -f es tu *farmer key*; mientras que el valor que le sigue a -p es tu *pool key*.

Una vez ejecutado el comando del título "Generar plots compatibles con una cuenta Chia", verás que Chia comienza a informarte qué está haciendo, del mismo modo que en la GUI podemos "Ver el log" del plot en procesamiento.
