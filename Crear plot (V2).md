# Crear un plot
## La forma correcta v2

Al menos en mi caso, cada plot no borra sus archivos temporales al finalizar. Esto ocasiona que, a mitad del plot siguiente (fase 2 de 4, probablemente) te quedes sin espacio en tu NVME de 512GB.
Claramente el momento en dónde salga el Error 1 "trying in five minutes" dependerá del tamaño de tu HDD/SSD/NVME. Este error dice que escribió unos bytes pero no pudo escribirlos todos, entonces intentará más tarde.
Para evitar este error frustrante y lograr un plotteo desatendido, dejo este script **createPlot** que pueden usar dentro de su carpeta *Chia CLI*.

```bash
echo "Eliminando archivos temporales en la carpeta '$1/*'..."
sleep 5
rm -R $1/*
echo "Comando 'rm' ejecutado"
chia plots create -k 32 -b 3390 -u 128 -r 2 -t $1 -d $2 -n 1 -f 99305144715663545df075d33322b313177fb41921746bbada3637912f6316ffbe3082bf1239f28d4eb8db80112b17f7 -p 82ae156f6c292e838da7324ed8f111ce904e66fed3478f3caa21a00113356e3ef7009d69d46c4e5348ef7d66ebaf23f5
```

Después de hacer *chmod +x createPlot*, llamarias al script de esta forma:

```bash
./createPlot /ruta/temporal /ruta/final
```

Si por alguna razón indicaste mal la carpeta temporal, tenés 5 segundos hasta que se efectúe el borrado de los elementos dentro de la carpeta que hayas indicado.

Ojo, el parámetro **-n** no supera el uno, porque en mi caso ordenar que se hagan más de un plot (añadiendose a la cola) genera [diversos problemas](https://github.com/Chia-Network/chia-blockchain/issues/3803).
