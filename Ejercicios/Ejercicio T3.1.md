## Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.

En windows podemos usar el comando:

`route ADD xxx.xxx.xxx.xxx MASK xxx.xxx.xxx.xxx  xxx.xxx.xxx.xxx `

siendo la primera IP la red a la que quieres acceder, la segunda la mascara de esa red y la tercera la puerta de enlace del router para acceder a esa red.

En linux podemos usar la herramienta iproute para añadior una ruta nueva para pasar el tráfico a otra subred:

`ip route add x.x.x.x/X via x.x.x.x`

donde la primera IP es la IP de la subred a la que queremos llegar con su máscara de red(dada por un entero) y la segunda IP es la puerta de enlace del router para acceder a esa red.

Referencias:

http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m6/enrutamiento_en_linux.html
http://linux-ip.net/html/tools-ip-route.html
http://www.howtogeek.com/howto/windows/adding-a-tcpip-route-to-the-windows-routing-table/