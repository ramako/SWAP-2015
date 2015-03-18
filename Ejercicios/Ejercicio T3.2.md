## Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

Para windows se puede usar su firewall, en Windows Server 2008 también podemos usar una herramienta que trae para filtrado de paquetes, dentro del panel de enrutamiento. También es posible descargarse un firewall propietario con opciones para bloqueo y filtrado de paquetes.

En linux pueden filtrarse y bloquearse los paquetes mediante la herramienta iptables. Para bloquear una IP por ejemplo:

`iptables -A INPUT -s x.x.x.x -j DROP`

Tráfico HTTP en la tarjeta de red eth0:

`iptables -A INPUT -i eth0 -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT`

Referencias:

https://technet.microsoft.com/es-es/library/cc732746%28v=ws.10%29.aspx

http://www.linuxtopia.org/Linux_Firewall_iptables/

http://www.thegeekstuff.com/2011/06/iptables-rules-examples/