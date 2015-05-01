## Discos en RAID


Creamos en Virtual Box los dos discos duros del mismo tamaño:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/RAIDVBox.png)

Instalamos el programa mdadm y creamos RAID:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/RAIDCreation.png)

Comprobamos el estado del RAID:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/RAIDstatus.png)

En principio traté de montarlo con el UUID, pero no funcionaba. Ademas, el fichero /etc/mdadm/mdadm.conf estaba vacio, asi que añadi manualmente el ARRAY md127 (el array md127 parece que se crea cuando hay algun problema aunque le hayamos indicado que queramos crear el md0):

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mdadm.png)

Añadi al fichero fstab la ultima linea para que dejase de dar error:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/fstab.png)

Comprobamos que al iniciarse esta montado:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/bootmount.png)

En la penúltima línea podemos ver que se ha montado automaticamente durante el arranque y no hemos necesitado introducir ningún comando.

Simulamos el fallo del disco duro:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/RAIDFail.png)

Retiramos el disco duro, comprobamos que podemos acceder a /datos y verificamos que el directorio /datos está montado en el RAID y que de verdad accedemos a traves de él:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/RAIDacceso.png)

Volvemos a conectar el disco duro y comprobamos que esté todo correcto:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/RAIDanadido.png)