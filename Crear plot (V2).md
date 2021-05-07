# Crear un plot
## La forma correcta v2

Si un plot o Chia tuvieron un error, no se borrarán los archivos temporales. Esto ocasiona que, a mitad del plot siguiente (fase 2 de 4, probablemente) te quedes sin espacio en tu NVME de 512GB (por ejemplo).

Claramente el momento en dónde salga el Error 1 "trying in five minutes" dependerá del tamaño de tu HDD/SSD/NVME. Este error dice que escribió unos bytes pero no pudo escribirlos todos, entonces intentará más tarde. 

---------------------------------------------

## Edit 07/05/2021
Algunos NVME no están diseñados para ser escritos por tanto tiempo. Ya sea porque no son SSDs para entornos empresariales y/o porque la temperatura de los chips sube mucho. Esto también puede generar el "Error 1" del cuál hablaba antes.

---------------------------------------------

Para evitar este error frustrante y lograr un plotteo desatendido, dejo este script **createPlot** que pueden usar dentro de su carpeta *Chia CLI* y en bucle. Por el momento

```bash
# $1 ruta temporal
# $2 ruta final
# $3 cantidad de plots
# -b -> 3390MB ram por defecto
# -r 2 (threads) por defecto
while :
do
        echo "Borrando $1..."
        sleep 5
        rm -R $1/*
        echo "Comando 'rm' ejecutado"
        chia plots create -k 32 -b 7168 -u 128 -r 4 -t $1 -d $2 -n 1 -f tuFarmerKey -p tuPoolKey
done
```

---------------------------------------------

Tenés que cambiar mi farmer key (-f) y pool key (-p) por la tuya.
Esto es muy importante porque los plots de una cuenta no son compatibles con otras. 

Por otro lado, aumentar el límite de RAM desde los 3390MB originales, ayudará en alrededor del 15%. HDDs lentos que tardaban +23hrs por plot usando 2 threads y 3390MB de RAM, ahora no pasan de las 20hrs. (15% de mejora, yay!)

---------------------------------------------


Después de hacer *chmod +x createPlot*, llamarias al script de esta forma:

```bash
./createPlot /ruta/temporal /ruta/final
```

Si por alguna razón indicaste mal la carpeta temporal, tenés 5 segundos hasta que se efectúe el borrado de los elementos dentro de la carpeta que hayas indicado.

## Plots en cola (param. -n)

Ojo, el parámetro **-n** no supera el uno, porque en mi caso ordenar que se hagan más de un plot (añadiendose a la cola) genera [diversos problemas](https://github.com/Chia-Network/chia-blockchain/issues/3803).

Por esta razón, el bucle *while* infinito va muy bien.
