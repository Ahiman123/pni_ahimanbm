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
R1(config)#router rip
R1(config-router)#network 192.168.2.0
R1(config-router)#network 192.168.1.0
R1(config-router)#
 ~~~

+ R2

 ~~~
R2(config)#router rip 
R2(config-router)#network 192.168.2.0
R2(config-router)#network 192.168.3.0
R2(config-router)#network 192.168.4.0
R2(config-router)#
 ~~~
 
+  R3

 ~~~
R3(config)#router rip
R3(config-router)#network 192.168.4.0
R3(config-router)#network 192.168.6.0
R3(config-router)#network 192.168.5.0
R3(config-router)#
 ~~~
 
 + R4
 
 ~~~
R4(config)#router rip 
R4(config-router)#network 192.168.6.0
R4(config-router)#network 192.168.7.0
R4(config-router)#network 192.168.8.0
R4(config-router)#
 ~~~
 
 + R5
 
 ~~~
R5(config)#router rip
R5(config-router)#network 192.168.8.0
R5(config-router)#network 192.168.9.0
R5(config-router)#
 ~~~

5. Muestra la tabla de enrutamiento del router **R3** para verificar si ha "aprendido" las redes de sus vecinos.

 + R3
 
 ~~~
 R3#show ip route 
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

R    192.168.1.0/24 [120/2] via 192.168.4.1, 00:00:26, Serial3/0
R    192.168.2.0/24 [120/1] via 192.168.4.1, 00:00:26, Serial3/0
R    192.168.3.0/24 [120/1] via 192.168.4.1, 00:00:26, Serial3/0
C    192.168.4.0/24 is directly connected, Serial3/0
C    192.168.5.0/24 is directly connected, FastEthernet0/0
C    192.168.6.0/24 is directly connected, Serial2/0
R    192.168.7.0/24 [120/1] via 192.168.6.2, 00:00:16, Serial2/0
R    192.168.8.0/24 [120/1] via 192.168.6.2, 00:00:16, Serial2/0
R    192.168.9.0/24 [120/2] via 192.168.6.2, 00:00:07, Serial2/0

R3#
 ~~~

 + Comprobar si la distancia a las redes se corresponde con la métrica. Considerando que en `RIP` la métrica es el número de saltos. Por ejemplo la red `192.168.8.0/24` debe tener métrica 2.
 + ¿Cual es la distancia administrativa de las redes aprendidas por `RIP`?

 + R3
 
 ~~~
 R    192.168.8.0/24 [120/1] via 192.168.6.2, 00:00:16, Serial2/0
 ~~~

6. Activar el modo de depuración en el router R2.

 + R2
 
 ~~~
 R2#RIP: received v1 update from 192.168.4.2 on Serial3/0
      192.168.5.0 in 1 hops
      192.168.6.0 in 1 hops
      192.168.7.0 in 2 hops
      192.168.8.0 in 2 hops
      192.168.9.0 in 3 hops
RIP: received v1 update from 192.168.2.1 on Serial2/0
      192.168.1.0 in 1 hops
RIP: sending  v1 update to 255.255.255.255 via FastEthernet0/0 (192.168.3.1)
RIP: build update entries
      network 192.168.1.0 metric 2
      network 192.168.2.0 metric 1
      network 192.168.4.0 metric 1
      network 192.168.5.0 metric 2
      network 192.168.6.0 metric 2
      network 192.168.7.0 metric 3
      network 192.168.8.0 metric 3
      network 192.168.9.0 metric 4
RIP: sending  v1 update to 255.255.255.255 via Serial2/0 (192.168.2.2)
RIP: build update entries
      network 192.168.3.0 metric 1
      network 192.168.4.0 metric 1
      network 192.168.5.0 metric 2
      network 192.168.6.0 metric 2
      network 192.168.7.0 metric 3
      network 192.168.8.0 metric 3
      network 192.168.9.0 metric 4
RIP: sending  v1 update to 255.255.255.255 via Serial3/0 (192.168.4.1)
RIP: build update entries
      network 192.168.1.0 metric 2
      network 192.168.2.0 metric 1
      network 192.168.3.0 metric 1
RIP: received v1 update from 192.168.4.2 on Serial3/0
      192.168.5.0 in 1 hops
      192.168.6.0 in 1 hops
      192.168.7.0 in 2 hops
      192.168.8.0 in 2 hops
      192.168.9.0 in 3 hops
RIP: received v1 update from 192.168.2.1 on Serial2/0
      192.168.1.0 in 1 hops
 ~~~

+ ¿Cuáles son las rutas las rutas enviadas por R2 a R1?

~~~
RIP: received v1 update from 192.168.2.1 on Serial2/0
      192.168.1.0 in 1 hops
~~~

+ ¿Cuáles son las rutas las rutas recibidas en R2 por parte de R3?

~~~
 R2#RIP: received v1 update from 192.168.4.2 on Serial3/0
      192.168.5.0 in 1 hops
      192.168.6.0 in 1 hops
      192.168.7.0 in 2 hops
      192.168.8.0 in 2 hops
      192.168.9.0 in 3 hops
RIP: received v1 update from 192.168.2.1 on Serial2/0
~~~

+ Razonar, analizando los apartados a y b, si funciona el horizonte dividido.

~~~
Sí funciona correctamente porque esta dando los saltos correspondientes
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

~~~
R2#show ip protocols 
Routing Protocol is "rip"
Sending updates every 30 seconds, next due in 23 seconds
Invalid after 180 seconds, hold down 180, flushed after 240
Outgoing update filter list for all interfaces is not set
Incoming update filter list for all interfaces is not set
Redistributing: rip
Default version control: send version 1, receive any version
  Interface             Send  Recv  Triggered RIP  Key-chain
  FastEthernet0/0       12 1
  Serial2/0             12 1
  Serial3/0             12 1
Automatic network summarization is in effect
Maximum path: 4
Routing for Networks:
	192.168.2.0
	192.168.3.0
	192.168.4.0
Passive Interface(s):
Routing Information Sources:
	Gateway         Distance      Last Update
	192.168.2.1          120      00:00:07
	192.168.4.2          120      00:00:14
Distance: (default is 120)
~~~

+ ¿ Qué versión se está enviando?

~~~
Se esta utilizando la version 1
~~~

+ ¿ Qué versión se acepta?

~~~
Se acpeta cualquier versión
~~~

+ ¿ Cada cuanto tiempo se envían las tablas de rutas ?

~~~
Cada 12 segundos
~~~

+ ¿ Qué redes están siendo publicadas por el `RIP` ?

~~~
Routing for Networks:
	192.168.2.0
	192.168.3.0
	192.168.4.0
~~~

+ ¿ Qué vecinos le están mandando información de enrutamiento?

~~~
Routing Information Sources:
	Gateway         Distance      Last Update
	192.168.2.1          120      00:00:07
	192.168.4.2          120      00:00:14
~~~




