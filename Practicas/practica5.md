## Replicación de bases de datos MySQL

Primero creamos la base de datos en nuestra máquina principal:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql.png)

Una vez hecho esto, debemos evitar que se acceda a la BD antes de crear la copia de seguridad:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql2.png)

Hacemos `su`
y ejecutamos el comando para crear la copia de seguridad:
`mysqldump contactos -u root -p > /home/contactos.sql `

Entramos en mysql y desbloqueamos las tablas con
`UNLOCK TABLES;

Copiamos el archivo desde la maquina en la que estara el backup mediante scp:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql3.png)


Si tratamos de insertar el fichero directamente, nos dirá que la base de datos no existe, por lo que tenemos que crearla manualmente.

Vemos que se ha creado y pasamos los datos contenidos en el fichero de la base de datos de esta manera:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql4.png)

Y comprobamos que se ha copiado correctamente:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/mysql5.png)
