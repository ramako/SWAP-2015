## Practica 3

# Creacion de la maquina e instalacion de nginx

He creado una nueva maquina virtual e instalado Ubuntu Server, para instalar nginx solo ha hecho falta:
`sudo apt-get install nginx`

Además del proceso para añadirla a la red interna de Virtual Box, he creado otro adaptador virtual para que sea visible desde mi anfitrión.
creando un adaptador solo anfitrión y levantando la nueva tarjeta de red desde el SO invitado.
`sudo ifconfig eth2 up`
`sudo dhclient eth2 ` para forzar la asignación de una IPv4 que son más faciles de trabajar con ellas.

Para la configuración de nginx como balanceador de carga:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/ubuntu%20server%203.png)

Al hacer dos curl a la ip de la maquina balanceadora de carga, vemos como alterna las páginas, sin embargo accediendo desde el anfitrión esto no ocurre con la frecuencia que debería.

He añadido weight=2 en la primera máquina, y de cada 3 conexiones 2 van a la primera máquina y 1a la segunda tanto desde el anfitrion como desde curl.



