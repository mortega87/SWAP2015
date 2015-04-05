##Ejercicios Tema 3

**Ejercicio T3.1: Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.**

Desde una terminal, el enrutamiento podemos visualizarlo ejecutando el comando:

**route -n**

Este nos muestra la tabla de rutas.

A través de las opciones del comando route podemos realizar más funciones, como por ejemplo, añadir una ruta estática a una red en la tabla de enrutamiento:

**route add -net <ip_destino> netmask <netmask> gw <puerta_enlace> dev eth0**

donde:

add -> Indica que la ruta se añade a la tabla de enrutamiento.

-net -> Indica que el destino es una red

-192.168.0.1 -> Indica la dirección IP de la red de destino

-netmask -> Indica la máscara de subred de la red de destino.

-gw 192.168.1.1 -> Indica el puerta de enlace de la red de destino.

-dev eth0 -> Indica que los paquetes se enrutan a través de la interfaz eth0.


O también podemos eliminar una ruta de la tabla de enrutamiento:

**route del -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.1.1 dev eth0**

El comando anterior eliminará la ruta a 192.168.1.0 de la tabla de enrutamiento.


**Ejercicio T3.2: Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.**

Cuando hacemos referencia al filtrado de paquetes, la principal herramienta en la que pensamos es un **firewall**.

Un firewall es una puerta de enlace de la red con filtro y sólo es eficaz en aquellos paquetes que deben pasar a través de ella. Por lo tanto, sólo puede ser eficaz cuando la única ruta para estos paquetes es a través del firewall.

El núcleo **Linux** incorpora el firewall **netfilter**. Puede controlarlo desde el espacio de usuario con los programas **iptables** e **ip6tables**. La diferencia entre estos dos programas es que el primero actúa sobre la red IPv4, mientras que el segundo actúa sobre IPv6. Debido a que ambas pilas de protocolos de red probablemente continuarán con nosotros durante muchos años, ambas herramientas son necesarias y deberán ser utilizadas en paralelo.

En **Windows**, el sistema operativo incorpora por defecto **Firewall de Windows**, donde a través de su interfaz podemos administrar funciones simples de su comportamiento.
