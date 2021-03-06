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

Aquí están las tablas con las medias de los  resultados, para la desviación estándar he utilizado [esta calculadora](http://www.alcula.com/es/calculadoras/estadistica/desviacion-estandar/).

Apache AB:

| Nginx balanceador    | Mediciones | Desviacion estándar |
|----------------------|------------|---------------------|
| Tiempo medio de test | 8.84476 ms |   0.168             |
| Failed request       | 3999       |   1490.56           |
| Requests per second  | 1130.974   |   21.50             |
| Time per request     | 88.4 ms    |   1.68              |


| Haproxy balanceador  | Mediciones |Desviacion estándar |
|----------------------|------------|---------------------|
| Tiempo medio de test | 7.333 ms   |    0.264             |
| Failed request       | 5000       |      0       |
| Requests per second  | 1385.27    |    52.822         |
| Time per request     | 72.26ms    |   2.64           |


| Sin balanceador      | Mediciones |Desviación estándar |
|----------------------|------------|--------------------|
| Tiempo medio de test | 4.39 ms    | 0.053 |
| Failed request       | 0          | 0 |
| Requests per second  | 2277.62    |27.298 |
| Time per request     | 43.91 ms   | 0.52 |

Gráficas

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/AB.jpg)


Estos resultados se antojan extraños debido a que los balanceadores deberían de 
dar mas rendimiento, sin embargo, han tenido mas peticiones fallidas que sin 
balanceador. Esto puede ser debido a la configuración del balanceador, una 
protección contra ataques DDoS, el servidor sobre el que funciona es menos 
potente que los servidores finales y no puede gestionar los balanceos, etc...

Aqui las tablas del programa httperf:

| Nginx balanceador    | Mediciones |Desviacion estándar |
|----------------------|------------|--------------------|
| Total connections    | 27000      | 0 |
| Replies              | 27000      | 0 |
| Request rate         | 150        | 0 |
| Errors total         | 0          | 0 |


| Haproxy balanceador  | Mediciones |Desviacion estándar |
|----------------------|------------|--------------------|
| Total connections    | 27000      | 0 |
| Replies              | 27000      | 0 |
| Request rate         | 150        | 0 |
| Errors total         | 0          | 0 |

| Sin balanceador      | Mediciones |Desviacion estándar |
|----------------------|------------|--------------------|
| Total connections    | 27000      |0 |
| Replies              | 27000      |0 |
| Request rate         | 150        |0 |
| Errors total         | 0          |0 |

Gráficas:

![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/httperf.jpg)

Los resultados, sorprendentemente, han sido los mismos. Quizás sea porque las máquinas no han sido estresadas a tope con este benchmark.

Aquí las tablas de OWL

| Nginx balanceador    | Mediciones | Desviación estándar|
|----------------------|------------|--------------------|
| Total TPS            | 999,2      | 62.83  |
| Avg response time    | 0,01       | 0.0007 |


| Haproxy balanceador  | Mediciones | Desviación estándar |
|----------------------|------------|---------------------|
| Total TPS            | 1104,91    | 42.90  |
| Avg response time    | 0,0092     | 0.0004 |


| Sin balanceador      | Mediciones | Desviación estándar |
|----------------------|------------|---------------------|
| Total TPS            | 1483,29    |69.003 |
| Avg response time    | 0,031      |0.0004 |


![](https://github.com/ramako/SWAP-2015/blob/master/Practicas/OWL.jpg)

Aquí se puede ver diferencia en el tiempo media de respuesta, siendo mas bajo en el caso de los balanceadores.
La media del número de peticiones completadas para la ejecución completa( Total TPS) es claramente mayor si no se usa balanceador, sin embargo el tiempo de respuesta medio es mucho más alto
que usando balanceadores.
