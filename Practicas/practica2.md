Aquí podemos ver las dos máquinas y como se copia el fichero tar mediante ssh de una a otra.

![Imgur](http://i.imgur.com/8GW8cue.png)

![Imgur](http://i.imgur.com/vkfu9j3.png)

Usamos rsync para copiar carpetas:

![Imgur](http://i.imgur.com/77lRuJV.png)

Generamos, copiamos las claves y comprobamos que podemos conectar sin password:

![Imgur](http://i.imgur.com/yr3NxQW.png)

Crontab:

![Imgur](http://i.imgur.com/w5syEIC.png)

Es posible que, en algunos casos, si lo ejecutamos como usuario normal, nos de problemas, asi que se puede sustituir el usuario que lo ejecuta por **root**

Es posible que al tratar de conectarnos por ssh como root nos de fallo aun poniendo la contraseña correcta, esto es debido a que por defecto la configuración por ssh no permite el logeo como root, hay que editar el fichero de configuración ssh del **servidor** al que nos conectamos, y cambiar PermitRootLogin a yes.
