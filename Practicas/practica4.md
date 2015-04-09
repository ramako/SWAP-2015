## Benchmarking de servidores web.
Con la granja web creada y los balanceadores de carga configurados de la 
práctica anterior, he utilizado las siguientes herramientas para el 
Benchmarking:

1. Apache AB
( `ab -n 1000 -c 10 ip-maquina/test.html `)
2. httperf (`httperf --client=0/1 --server=192.168.56.10x -- port=80 --uri=/index.html --rate=150  --num-conn=27000 --num-call=1 --timeout=5 `)
3. Open Web Loader
(`openload http://192.168.56.10x/index.html 10` )

En httperf y OWL sustituyo la x final por la ip de la máquina o balanceador.

Para cada una de estas herramientas, las he ejecutado contra

1. nginx
2. haproxy
3. Apache (sin balanceo de carga)

La máquina virtual que sirve como balanceo de carga está configurada para que 
sea vista desde el anfitrión-
Para Apache AB he utilizado 10000 conexiones y 1000 concurrentes.

Aquí están las tablas con las medias de los  resultados.


| Nginx balanceador    | Mediciones |
|----------------------|------------|
| Tiempo medio de test | 8.84476 ms |
| Failed request       | 3999       |
| Requests per second  | 1130.974   |
| Time per request     | 88.4 ms    |


| Haproxy balanceador  | Mediciones |
|----------------------|------------|
| Tiempo medio de test | 7.333 ms   |
| Failed request       | 5000       |
| Requests per second  | 1385.27    |
| Time per request     | 72.26ms    |


| Sin balanceador      | Mediciones |
|----------------------|------------|
| Tiempo medio de test | 4.39 ms    |
| Failed request       | 0          |
| Requests per second  | 2277.62    |
| Time per request     | 43.91 ms   |

Gráficas

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/AB.jpg)


Estos resultados se antojan extraños debido a que los balanceadores deberían de 
dar mas rendimiento, sin embargo, han tenido mas peticiones fallidas que sin 
balanceador. Esto puede ser debido a la configuración del balanceador, una 
protección contra ataques DDoS, el servidor sobre el que funciona es menos 
potente que los servidores finales y no puede gestionar los balanceos, etc...

Aqui las tablas del programa httperf:

| Nginx balanceador    | Mediciones |
|----------------------|------------|
| Total connections    | 27000      |
| Replies              | 27000      |
| Request rate         | 150        |
| Errors total         | 0          |


| Haproxy balanceador  | Mediciones |
|----------------------|------------|
| Total connections    | 27000      |
| Replies              | 27000      |
| Request rate         | 150        |
| Errors total         | 0          |

| Sin balanceador      | Mediciones |
|----------------------|------------|
| Total connections    | 27000      |
| Replies              | 27000      |
| Request rate         | 150        |
| Errors total         | 0          |

Gráficas:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/httperf.jpg)

Los resultados, sorprendentemente, han sido los mismos.

Aquí las tablas de OWL

| Nginx balanceador    | Mediciones |
|----------------------|------------|
| Total TPS            | 999,2      |
| Avg response time    | 0,01       |


| Haproxy balanceador  | Mediciones |
|----------------------|------------|
| Total TPS            | 1104,91    |
| Avg response time    | 0,0092     |


| Sin balanceador      | Mediciones |
|----------------------|------------|
| Total TPS            | 1483,29    |
| Avg response time    | 0,031      |


![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/OWL.jpg)

Aquí se puede ver diferencia en el tiempo media de respuesta, siendo mas bajo en el caso de los balanceadores.
La media del número de peticiones completadas para la ejecución completa( Total TPS) es claramente mayor si no se usa balanceador. 
