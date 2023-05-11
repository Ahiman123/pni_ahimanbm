# ENRUTAMIENTO DINÁMICO RIP V1

Dada la siguiente topología de red:

![](img/001.png)

1. Crear el siguiente esquema de red usando el ***Packet Tracert***. Configurar las interfaces de cada router y asignarle una dirección `IP` por cada interfaz.

2. Activar el protocolo `RIP` en cada uno de los routers de la figura de arriba.

+ R1

 ~~~
R1(config)#router rip
 ~~~

+ R2

 ~~~
R2(config)#router rip
 ~~~
 
 + R3
 
 ~~~
R3(config)#router rip
 ~~~
 
 + R4
 
 ~~~
R4(config)#router rip
 ~~~
 
 + R5
 
 ~~~
R5(config)#router rip
 ~~~

3. Publicar las redes con el protocolo `RIP` en cada una de los routers. 

+ R1

 ~~~
R1(config-router)#
 ~~~

+ R2

 ~~~
R2(config-router)#
 ~~~
 
+  R3

 ~~~

 ~~~
 
 + R4
 
 ~~~
 ~~~
 
 + R5
 
 ~~~
 ~~~

5. Muestra la tabla de enrutamiento del router **R3** para verificar si ha "aprendido" las redes de sus vecinos.

 + R3
 
 ~~~
 ~~~

 + Comprobar si la distancia a las redes se corresponde con la métrica. Considerando que en `RIP` la métrica es el número de saltos. Por ejemplo la red `192.168.8.0/24` debe tener métrica 2.
 + ¿Cual es la distancia administrativa de las redes aprendidas por `RIP`?

 + R3
 
 ~~~
 ~~~

6. Activar el modo de depuración en el router R2.

 + R2
 
 ~~~
 ~~~

+ ¿Cuáles son las rutas las rutas enviadas por R2 a R1?

~~~
~~~

+ ¿Cuáles son las rutas las rutas recibidas en R2 por parte de R3?

~~~
~~~

+ Razonar, analizando los apartados a y b, si funciona el horizonte dividido.

~~~
~~~

7. Como se observa en el esquema de red, por la parte de la red Ethernet no hay ningún router, por tanto, se quiere evitar que el router no mande tráfico `RIP` por esa interfaz, ¿Qué se debe de hacer?

 + R1
 
 ~~~
 ~~~

+ R2

 ~~~
 ~~~
 
 + R3
 
 ~~~
 ~~~
 
 + R4
 
 ~~~
 ~~~
 
 + R5
 
 ~~~
 ~~~

8. Usando `show ip protocolos` en el router R2 y contestar a las siguientes preguntas:

+ ¿ Qué versión se está enviando?

~~~
~~~

+ ¿ Qué versión se acepta?

~~~
~~~

+ ¿ Cada cuanto tiempo se envían las tablas de rutas ?

~~~
~~~

+ ¿ Qué redes están siendo publicadas por el `RIP` ?

~~~
~~~

+ ¿ Qué vecinos le están mandando información de enrutamiento?

~~~
~~~




