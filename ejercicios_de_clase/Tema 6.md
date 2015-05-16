##Ejercicios Tema 6

**Ejercicio T6.1: Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas.
Comprobar el funcionamiento.
Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas.
Comprobar el funcionamiento.**

Para bloquear el tráfico entrante con iptables podemos utilizar el siguiente comando.

<pre>iptables -P INPUT DROP</pre>

Ejecutamos el comando y hacemos una petición a las maquinas servidoras y vemos que queda en estado bloqueado en la siguiente:

![](./img/6.1)

Volvemos a aceptar las peticiones con:

<pre>iptables -P INPUT ACCEPT</pre>

Y vemos como vuelve a aceptar son problema peticiones web de servidores externos.

![](./img/6.2)


**Ejercicio T6.2:
Comprobar qué puertos tienen abiertos nuestras máquinas, su estado, y qué programa o demonio lo ocupa.**

Podemos comprobarlo ejecutando en una de nuestras máquinas servidoras el comando:

<pre>netstat -tulpn</pre>

![](./img/6.3)

**Ejercicio T6.3:
Buscar información acerca de los tipos de ataques más comunes en servidores web, en qué consisten, y cómo se pueden evitar.**


Hay dos tipos de ataques a servidores web, a nivel de sistema y a nivel de aplicacion:

**Nivel de Sistema**.

Es el nivel de acceso que representa más riesgo. Es lo que todo intruso desea lograr en una máquina: tener el control total de los recursos... adueñarse completamente de la máquina con los mismos privilegios que el propio administrador.
El acceso a nivel de sistema implica el acceso al mismo sistema operativo, en última instancia mediante un terminal remoto.
Estos accesos se logran a través de algún servicio mal configurado, o de aplicaciones vulnerables que permitan la ejecución de código arbitrario en el server. Por ejemplo: si tenemos abierto un servicio telnet, o un SSH vulnerable, estamos dando al atacante una terminal de acceso para que simplemente comience a trabajar en su próximo paso que discutiremos en las próximas líneas: la escalada de privilegios.
Otra posible entrada a un sistema es la explotación de servicios vulnerables que permitan desbordamientos de búfers (que nos permitan, aún sin tener un terminal, ejecutar comandos en el sistema operativo).


**Nivel de Aplicación.**

Los ataques a nivel de aplicación son aquellos que se realizan explotando vulnerabilidades de aplicaciones que permitan modificar los datos que la propia aplicación manipula, pero sin la posibilidad de ejecución de comandos sobre el sistema operativo.
Ejemplos: la modificación o borrado de contenidos en un sistema de gestión de portales, como phpNuke o Mambo. O la manipulación de una base de datos SQL mediante un acceso no autorizado a un phpMyAdmin vulnerable.
En este tipo de ataques el intruso puede cambiar lo que desee en nuestro sitio web, o en nuestras bases de datos. Pero no se puede considerar que el servidor esté comprometido, ni que el intruso haya entrado efectivamente en el sistema.
Los ataques a nivel de aplicación son los más comunes y visibles (y los más populares entre los chicos traviesos aficionados a romper cosas). De modo que el servidor -a pesar de estos ataques- permanece intacto. La seriedad y la gravedad de estos ataques depende de la importancia de la aplicación web atacada: no es lo mismo un ataque de este tipo en una galería de fotos online, que en una aplicación de procesamiento de pagos y transferencias financieras.


**Conclusiones.**

En el caso de las intrusiones a nivel de sistema, se debe realizar un análisis forense del servidor atacado. Y en muchos casos, la única solución realmente segura es la reinstalación del sistema operativo y de todas las aplicaciones desde cero.
En el caso de las intrusiones a nivel de aplicación, basta con sustituír la aplicación vulnerable por una versión "parcheada" que cierre las brechas de seguridad usadas por los intrusos.
