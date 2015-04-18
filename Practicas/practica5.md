## Replicación de bases de datos MySQL

Primero creamos la base de datos en nuestra máquina principal:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql.png)

Una vez hecho esto, debemos evitar que se acceda a la BD antes de crear la copia de seguridad:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql2.png)

Hacemos `su`
y ejecutamos el comando para crear la copia de seguridad:
`mysqldump contactos -u root -p > /home/contactos.sql `

Entramos en mysql y desbloqueamos las tablas con
`UNLOCK TABLES;`

Copiamos el archivo desde la maquina en la que estara el backup mediante scp:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql3.png)


Si tratamos de insertar el fichero directamente, nos dirá que la base de datos no existe, por lo que tenemos que crearla manualmente.

Vemos que se ha creado y pasamos los datos contenidos en el fichero de la base de datos de esta manera:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql4.png)

Y comprobamos que se ha copiado correctamente:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql5.png)

### Replicacion automatica.

Configuramos el maestro

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql-master.png)

y reiniciamos el servicio mysql:
`/etc/init.d/mysql restart`

Nos vamos al servidor de backup y configuramos lo mismo pero con server-id = 2

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql-esclavo.png)

Y añadimos las lineas para configurar la conexión al maestro, pero al reiniciar el servicio nos da un error, comprobamos la versión de y mysql y es la version 5.5, luego habrá que configurarlo desde la consola de mysql.

En el master escribimos:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql-master2.png)

Entramos en el esclavo y en la consola mysql escribimos:

```
CHANGE MASTER TO MASTER_HOST='192.168.1.100',
MASTER_USER='esclavo', MASTER_PASSWORD='esclavo',
MASTER_LOG_FILE='mysql-bin.000003', MASTER_LOG_POS=501,
MASTER_PORT=3306;
```

Comprobamos que funciona:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql-esclavo2.png)

Y ejecutando una sentencia para insertar validamos que se replica automaticamente:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysqlfuncionando.png)
