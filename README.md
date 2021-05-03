# Guía de Chia coin (Linux)

Para instalar Chia (usable desde CLI) para Linux/Mac, seguir [este tutorial](https://github.com/Chia-Network/chia-blockchain/wiki/INSTALL). En Windows, el instalador pondrá la interfaz visual y la versión de consola, todo-en-uno.

## Iniciar una cuenta nueva

Una vez que instalás Chia en tu sistema operativo, ejecutá el comando.
1. Para Linux/Mac

```bash
$ cd /ruta/a/carpeta/de/chia-blockchain
$ . ./activate # Inicia el entorno de Chia
$ chia init # Crea una cuenta nueva
```

2. Para Windows 10

```bash
$ cd "C:\Users\tuUsuario\AppData\Local\chia-blockchain\app-1.1.3\resources\app.asar.unpacked\daemon\"
```

---------------------------------------------------------------

Revisar la parte dónde dice "app-1.1.3" y cambiarla por la versión que tengas instalada (hoy 03/05/2021, es la última disponible).

---------------------------------------------------------------

En caso de que la cuenta se cree, pero no te muestre tus claves privadas y/o la frase mnemónica, este comando lo hará:

```bash
chia keys show --show-mnemonic-seed
```

Guardá todo el output generado por el comando anterior (tales cómo master public y private key, farmer public key, pool public key, Mnemonic seed, etc) en algún lugar seguro. Por ejemplo, yo copio y pego ese contenido en un archivo de texto y luego lo comprimo en formato 7z, encriptado con contraseña.

## Uso de estas keys
* Master public key: es una clave pública que podés compartir con cualquier persona y permite ver tu billetera en modo sólo lectura, es decir, quién tenga esta clave **no** puede transferir tu dinero a otro lado, administrar los plots, etc.
* Farmer public key: es una clave pública para que otros dispositivos puedan generar plots compatibles con tu cuenta Chia, y así poder plotear en simultáneo en varias máquinas para luego tener una PC que use esos plots para minar.
* Pool public key: esta clave pública trabaja en conjunto con *Farmer public key*.
* Mnemonic seed: son 24 palabras que se usan para restaurar completamente tu cuenta Chia (modo lectura/escritura, dando todos los permisos para administrar tus fondos y plots).

## Generar plots sin exponer la private key

Gracias a Chia CLI, podemos crear plots afines a una cuenta en particular en una computadora ajena/pública, sin necesidad de exponer la *private key* de dicha cuenta. A continuación verás los métodos en Linux/Mac y Windows.

## Generar plots compatibles con una misma cuenta Chia (Linux/Mac)

Abrí una terminal (Linux/Mac) y escribí los siguientes comandos, teniendo en cuenta que si la ruta a una carpeta **contiene espacios**, debe ir **entre comillas**:

```bash
$ cd /ruta/a/carpeta/de/chia-blockchain
$ . ./activate
$ chia plots create -k 32 -b 3390 -u 128 -r 2 -t /ruta/temporal -d /ruta/final -n 1 -f 99305144715663545df075d33322b313177fb41921746bbada3637912f6316ffbe3082bf1239f28d4eb8db80112b17f7 -p 82ae156f6c292e838da7324ed8f111ce904e66fed3478f3caa21a00113356e3ef7009d69d46c4e5348ef7d66ebaf23f5
```

¡Bien! Ya está comenzando el proceso del plot.

## Generar plots compatibles con una misma cuenta Chia (Windows)

La ruta de Chia CLI en Windows es un tanto distinta, y el instalador de este SO trae Chia Electron (GUI) y Chia CLI (para ejecutar comandos en consola) todo-en-uno. A día de hoy, la herramienta en consola es mucho más estable y permite más opciones, como crear plots para una cuenta determinada sólo con su farmer y pool key. Esta característica es útil por si queremos crear plots para una cuenta propia y sin exponer nuestra *private key*.

Primero nos dirijimos a la carpeta dónde está Chia CLI, teniendo en cuenta que la ruta debe estar **entre comillas**:

```bash
$ cd "C:\Users\tuUsuario\AppData\Local\chia-blockchain\app-1.1.3\resources\app.asar.unpacked\daemon\"
```

Revisar la parte dónde dice "app-1.1.3" y cambiarla por la versión que tengas instalada (hoy 03/05/2021, es la última disponible). Una vez allí, podemos correr el mismo comando en Linux, con una ligera diferencia: en PowerShell se anteponen los símbolos **./** antes de escribir "*chia*", así:

```bash
$ ./chia plots create -k 32 -b 3390 -u 128 -r 2 -t /ruta/temporal -d /ruta/final -n 1 -f 99305144715663545df075d33322b313177fb41921746bbada3637912f6316ffbe3082bf1239f28d4eb8db80112b17f7 -p 82ae156f6c292e838da7324ed8f111ce904e66fed3478f3caa21a00113356e3ef7009d69d46c4e5348ef7d66ebaf23f5
```

¡Bien! Ya está comenzando el proceso del plot.

## Entender los parámetros enviados a Chia
**plots create** es la llamada a una función interna de la wallet Chia, que se encarga de crear plots. Los parámetros *-k*, *-b*, *-u* y *-r* te recomiendo no tocarlos a pesar de que tengas una PC "ploteadora" muy potente. Añadir más threads de procesamiento (aumentando el valor que le sigue a *-r* no aumentó la velocidad al crear plots. De hecho, más de 4 threads lo empeora.
Para saber en detalle qué hacen los parámetros *-t*, *-d*, *-n*, *-f* y *-p*, escribí el comando **chia plots create -h**, pero el valor que le sigue a la -f es tu *farmer key*; mientras que el valor que le sigue a -p es tu *pool key*. Reemplazando estos dos últimos valores por tu farmer y pool key, podrás plotear para tu cuenta sin problema.

Una vez ejecutado el comando del título "Generar plots compatibles con una cuenta Chia", verás que Chia comienza a informarte qué está haciendo, del mismo modo que en la GUI podemos "Ver el log" del plot en procesamiento.
