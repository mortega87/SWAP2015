##Ejercicios Tema 2

**Ejercicio T2.1: Calcular la disponibilidad del sistema descrito en edgeblog.net si tenemos dos réplicas de cada elemento salvo para el centro de datos (en total 3 elementos en cada subsistema).**

Según la tabla de disponibilidades en los subsistemas, si queremos calcular la disponibilidad del sistema con dos réplicas por cada subsistema, realizamos los siguientes cálculos:

**WEB**

Réplica 1 -> 85%+(1-85%)*85% = 97.75%

Réplica 2 -> 97.75%+(1-97.75%)*85% = 99.6625%


**APPLICATION**

Réplica 1 -> 90%+(1-90%)*90% = 99%

Réplica 2 -> 99%+(1-99%)*90% = 99.9%


**DATABASE**


Réplica 1 -> 99.9%+(1-99.9%)*99.9% = 99.9999%

Réplica 2 -> 99.9999%+(1-99.9999%)*99.9% = 99.9999999%


**DNS**

Réplica 1 -> 98%+(1-98%)*98% = 99.96%

Réplica 2 -> 99.96%+(1-99.96%)*98% = 99.9992%


**FIREWALL**

Réplica 1 -> 85%+(1-85%)*85% = 97.75%

Réplica 2 -> 97.75%+(1-97.75%)*85% = 99.6625%


**SWITCH**

Réplica 1 -> 99%+(1-99%)*99% = 99.99%

Réplica 2 -> 99.99%+(1-99.99%)*99% = 99.999999%

**ISP**

Réplica 1 -> 95%+(1-95%)*95% = 99.75%

Réplica 2 -> 99.75%+(1-99.75%)*95% = 99.9875%

Una vez calculada la disponibilidad de cada componente replicado 2 veces, excepto el Data Center, calculamos la disponibilidad total del sistema.

Disponibilidad_total=99.6625% x 99.9% x  99.9999999% x 99.9992% x 99.6625% x 99.999999% x  99.9875% = 99.2136%


**Ejercicio T2.2: Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. Como ejemplo, examina PM2: https://github.com/Unitech/pm2 que sirve para administrar clústeres de NodeJS.**

Django es un framework web muy potente que ya he utilizado en una práctica para una asignatura, en la cual administrábamos funcionalidades de un servidor y consultábamos características de éste. El lenguaje para el que se utiliza es python. Una libreria bastante util es Paramiko, con la que podemos realizar ssh a traves de nuestra aplicación web, asociandolo a algún evento de la web.


**Ejercicio T2.3: ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor? Buscar herramientas y aprender a usarlas.**

Existen muchas herramientas en el mercado que satisfacen este propósito. Voy a nombrar dos de código abierto.

**ApacheBench**

Esta herramienta como su nombre lo indica nos la entrega la fundación Apache y ofrece múltiples opciones, además viene preinstalada en los sistemas Mac OS X.

Para instalarlo en sistemas Linux basados en Debian basta con ejecutar el siguiente comando:

$ sudo apt-get install apache2-utils

Ahora solo queda empezar a probar contra un servidor. Ya que no queremos que nos bloqueen de ningún sitio por estar atacándolo sin merced, lo haremos contra uno local.

El formato más común para realizar una prueba es algo como esto:

$ ab -n 10000 -c 100 -g grafica.data http://localhost:8888/loadTesting/test

ab nos permite hacer uso de la herramienta.

-n especificamos la cantidad de peticiones que deseamos enviar.

-c especificamos la cantidad de conexiones concurrentes.

-g podemos generar una gráfica de gnuplot para apreciar mejor los resultados.

Finalmente colocamos la dirección que deseamos probar.

Tendríamos como resultado una salida así:

<pre>
This is ApacheBench, Version 2.3 <$Revision: 1373084 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 1000 requests
Completed 2000 requests
Completed 3000 requests
Completed 4000 requests
Completed 5000 requests
Completed 6000 requests
Completed 7000 requests
Completed 8000 requests
Completed 9000 requests
Completed 10000 requests
Finished 10000 requests


Server Software:        Apache/2.2.22
Server Hostname:        localhost
Server Port:            8888

Document Path:          /loadTesting/test
Document Length:        43 bytes

Concurrency Level:      100
Time taken for tests:   68.749 seconds
Complete requests:      10000
Failed requests:        0
Write errors:           0
Total transferred:      6660000 bytes
HTML transferred:       430000 bytes
Requests per second:    145.46 [#/sec] (mean)
Time per request:       687.489 [ms] (mean)
Time per request:       6.875 [ms] (mean, across all concurrent requests)
Transfer rate:          94.60 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0  152 154.5    108     598
Processing:    16  533 287.5    520    2137
Waiting:        1  487 283.0    483    2063
Total:         87  685 259.6    618    2425

Percentage of the requests served within a certain time (ms)
  50%    618
  66%    733
  75%    835
  80%    905
  90%   1045
  95%   1154
  98%   1318
  99%   1475
 100%   2425 (longest request)
</pre>

Podemos apreciar varios datos de interés como:

Tiempos promedio de peticiones por segundo.
Tiempo promedio para cumplir una petición.
Velocidad de transferencia.
Tiempos por estado de petición.


**Siege**

Una herramienta utilizada ampliamente por desarrolladores (y algunos hacktivistas) para realización de pruebas de carga. Cortesía de JoeDog Software

En Debian Linux se puede instalar con:
	<pre>sh $ apt-get install siege</pre>

Hagamos una prueba parecida a la que hicimos con ApacheBench:

$ siege -t 60s -c 100 -b -q http://localhost:8888/loadTesting/test
siege nos permite hacer uso de la herramienta.

-t especificamos el tiempo que tomará la prueba.

-c especificamos la cantidad de conexiones concurrentes.

-b obliga a no tener ningún retraso entre cada usuario simulado (modo benchmark).

-q elimina la salida resultante de cada petición que va mostrando el proceso durante la prueba.

Finalmente colocamos la dirección que deseamos probar.

Tendríamos como resultado una salida así:

<pre>
Transactions:             7718 hits
Availability:             100.00 %
Elapsed time:             59.83 secs
Data transferred:           0.32 MB
Response time:              0.77 secs
Transaction rate:           129.00 trans/sec
Throughput:               0.01 MB/sec
Concurrency:              98.97
Successful transactions:        7718
Failed transactions:             0
Longest transaction:          2.74
Shortest transaction:         0.02
</pre>

También podemos especificar con el atributo -f la ruta a un archivo donde puedes especificar múltiples direcciones que deseas atacar en la misma prueba, además el atributo -d permite colocar un intervalo de retraso entre cada usuario simulado, lo cual simularía un comportamiento más natural.



**Ejercicio T2.4: En este ejercicio debemos buscar diferentes tipos de productos: (1) Buscar ejemplos de balanceadores software y hardware (productos comerciales). (2) Buscar productos comerciales para servidores de aplicaciones. (3) Buscar productos comerciales para servidores de almacenamiento.**

**(1)**Como hemos utilizado en la pŕactica 3, dos software de balanceador de carga bastante extendidos son nginx, que a pesar de ser un servidor web, posee tambien este servicio, y haproxy, de software libre que actúa como balanceador de carga ofreciendo alta disponibilidad, balanceo de carga y proxy para comunicaciones TCP y HTTP. Otros balanceadores muy extendidos son Linux Virtual Servers, Pound y Pen. Coomo balanceador hardware podemos consultar el TP-Link TL-R470T+ Balanceador de carga 4 WAN en el siguiente enlace http://www.comprawifi.com/routers-aps-switch/balanceador/tp-link-tl-r470t-balanceador-de-carga-4-wan/prod_2796.html

**(2)** Debido a la extensión del lenguaje Java en el campo de desarrollo de aplicaciones, podemos encontrar bastantes servidores de aplicaciones asociados que hacen referencia a un servidor de aplicaciones Java EE. Entre los servidores de aplicación Java EE privativos más conocidos se encuentran **WebLogic** de Oracle y **WebSphere** de IBM. **EAServer** de Sybase Inc. es también conocido por ofrecer soporte a otros lenguajes diferentes a Java, como PowerBuilder. Entre los servidores de aplicaciones libres se encuentran **JOnAS** del consorcio ObjectWeb, **JBoss AS** de JBoss (división de Red Hat), **Geronimo** de Apache, **TomEE** de Apache, **Resin Java Application Server** de Caucho Technology, **Blazix** de Desiderata Software, **Enhydra Server** de Enhydra.org y **GlassFish** de Oracle.

**(3)**La importante empresa **WD** posee multitud servidores de almacenamiento, como podemos ver consultando el siguiente enlace: http://www.wdc.com/sp/products/business/Windows-Storage-Servers/. Tambien posee una gran variedad **OVH** https://www.ovh.es/servidores_dedicados/almacenamiento/. Hoy dia el almacenamiento el cloud se extá extendiendo a pasos agigantados, y podemos obtener un servidor fiable y con buen soporte gracias, por ejemplo, a **Windows Azure**.
