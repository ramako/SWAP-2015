## Practica 3

# Creacion de la maquina e instalacion de nginx

He creado una nueva maquina virtual e instalado Ubuntu Server, para instalar nginx solo ha hecho falta:
`sudo apt-get install nginx`

Adem�s del proceso para a�adirla a la red interna de Virtual Box, he creado otro adaptador virtual para que sea visible desde mi anfitri�n.
creando un adaptador solo anfitri�n y levantando la nueva tarjeta de red desde el SO invitado.
`sudo ifconfig eth2 up`
`sudo dhclient eth2 ` para forzar la asignaci�n de una IPv4 que son m�s faciles de trabajar con ellas.

Para la configuraci�n de nginx como balanceador de carga:

URL SCREENSHOT AQU�

Al hacer dos curl a la ip de la maquina balanceadora de carga, vemos como alterna las p�ginas, sin embargo accediendo desde el anfitri�n
esto no ocurre con la frecuencia que deber�a.

He a�adido weight=2 en la primera m�quina, y de cada 3 conexiones 2 van a la primera m�quina y 1a la segunda tanto desde el anfitrion como
desde curl.

