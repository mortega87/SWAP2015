###Práctica 3 SWAP

En primer lugar, vamos a **instalar nginx** en nuestra tercera máquina Ubuntu Server.
Para ello, vamos primero a importar la clave del repositorio de la siguietne forma:

![](./img/1.png)

Y a continuación, editamos el fichero sources.list para agregar los paquetes al repositorio.

![](./img/2.png)

Para terminar con la instalación del servidor web nginx, ejecutamos el siguiente comando y tras aceptar la instalación, ya tendremos nginx en nuestro servidor.

![](./img/3.png)

Una vez finalizada la instalación, lo **configuramos como balanceador de carga** de la siguiente manera:

Creamos el fichero default.conf en la ruta /etc/nginx/conf.d/ y definimos, como vemos en la imagen, las máquinas que van a formar parte del clúster web, en este caso las máquinas virtuales servidoras creadas en prácticas anteriores.

En este fichero especificamos las ip's de dichas máquinas.

![](./img/4.png)

A continuación, a este mismo fichero, y posterior a la sección server, le indicamos, como muestro en al siguiente imagen, la configuración para indicarle que use el grupo definido anteriormente (upstream).

![](./img/5.png)

Reiniciamos el servicio nginx para que tome la nueva configuración:

<pre>service nginx restart</pre>

Y comprobamos que funciona correctamente realizando peticiones web a una de las máquinas servidoras, en este caso la máquina 2.

![](./img/6.png)

Ahora vamos a asignarle el doble de peso a la máquina 1, que tiene la ip 192.168.1.100, con la propiedad weight.

![](./img/7.png)

Comprobamos que realizando una petición web a la máquina principal, sigue funcionando correctamente.


![](./img/8.png)
