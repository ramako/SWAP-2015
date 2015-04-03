## Benchmarking de servidores web.
Con la granja web creada y los balanceadores de carga configurados de la 
práctica anterior, he utilizado las siguientes herramientas para el 
Benchmarking:
1. Apache AB
2. httperf
3. Open Web Loader

Para cada una de estas herramientas, las he ejecutado contra

1. nginx
2. haproxy
3. Apache (sin balanceo de carga)

La máquina virtual que sirve como balanceo de carga está configurada para que 
sea vista desde el anfitrión-
Para Apache AB he utilizado 10000 conexiones y 1000 concurrentes.

Aquí están las tablas con los resultados (la media de 5 ejecuciones).


| Nginx balanceador    | Mediciones |
|----------------------|------------|
| Tiempo medio de test | 8.84476 ms |
| Failed request       | 3999       |
| Requests per second  | 1130.974   |
| Time per request     | 88.4 ms    |


| Haproxy balanceador  | Mediciones |
|----------------------|------------|
| Tiempo medio de test | 8.84476 ms |
| Failed request       | 5000       |
| Requests per second  | 1385.27    |
| Time per request     | 72.26ms    |


| Sin balanceador      | Mediciones |
|----------------------|------------|
| Tiempo medio de test | 4.39 ms    |
| Failed request       | 0          |
| Requests per second  | 2277.62    |
| Time per request     | 43.91 ms   |


Estos resultados se antojan extraños debido a que los balanceadores deberían de 
dar mas rendimiento, sin embargo, han tenido mas peticiones fallidas que sin 
balanceador. Esto puede ser debido a la configuración del balanceador, una 
protección contra ataques DDoS, el servidor sobre el que funciona es menos 
potente que los servidores finales y no puede gestionar los balanceos, etc...