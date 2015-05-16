##Ejercicios Tema 5

**Ejercicio 5.1: Buscar información sobre cómo calcular el número de conexiones por segundo.**

Para saber el número de conexiones por segundo que está crusandp el servidor, si es **Apache**, podemos utilizar el siguiente comando.

<pre>apache2ctl status | grep request</pre>

Tambiés es posible observar el tráfico mediante **netstat**. Sin embargo, no nos ofrece mayor información sobre el enrutamiento de los paquetes.  Para esto tenemos **iptstate**, el cual, nos ofrece información de las conexiones entrantes, salientes y reenviadas (o enrutadas). Con lo que podremos determinar las direcciones IP fuente y destino, ambos con su respectivo puerto, protocolo, estado de la conexión y el TTL.

Puedes también filtrar la salida del comando para que te diga el número de conexiones a un puerto determinado de una dirección IP, por ejemplo:

<pre>iptstate -1 -d 192.168.0.100 -D 80</pre>


**Ejercicio 5.2: Instalar wireshark y observar cómo fluye el tráfico de red en uno de los servidores web mientras se le hacen peticiones HTTP.**

He intentado con wireshark mostrar la traza de las máquinas servidoras creadas para las prácticas, pero me ha sido imposible mostrar los datos. Imagino que será por un problema con VirtualBox.


**Ejercicio 5.3: Buscar información sobre características, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.**

Para monitorizar prestaciones de servidores desde el sistema operativo he encontrado estas tres herramientas:

La primera herramienta, **Loadimpact**, permite medir la carga de usuarios simultáneos que puede soportar tu página  web.

Esta herramienta es muy útil para conocer los recursos del servidor o ver el tráfico del servidor.

La segunda herramienta, **Pingdom** es una herramienta de monitorización que usamos, sobre todo, para dos cosas:

1. Para monitorizar la disponibilidad del servidor.

2. Para monitorizar los tiempos de respuesta del servidor.

Por último, **Web Page Test** es una herramienta muy  potente y completa que analiza la carga una página web proporcionando un desglose extremadamente detallado de los proceso de carga con una información que es muy valiosa, por ejemplo, para depurar un sitio web detectando cuellos de botella que ralentizan la velocidad del sitio y problemas técnicos que están impactando negativamente el proceso de carga.
