# Manual de Configuración. 
Redes de Computadoras 1 - Practica 4

## Topología de Red

La topología que se implemento en esta práctica esta compuesta por:

1. **VPC**
2. **Switch**
3. **Ether-switch**
4. **Router**
5. **Maquina Virtual**

### Configuración de Topología

La topologia esta compuesta principalmente por un solo router, 2 switch, 2 etherswitch, 2 VPC y una maquina virtual. 

Las conexiones entre los equipos estan dadas de la siguiente forma. 

|Tipo de Host     |Nombre       | Conectado a         |Puerto/Interfaz  |
| --------------- | ----------- | --------------------|---------------- |
|VPC              |PC1          |Switch1              |Ethernet0        |
|VPC              |PC2          |Switch2              |Ethernet0        |
|VPC              |PC3          |Switch2              |Ethernet0        |
|Máquina Virtual  |TinyLinuxVM-1|Switch1              |Ethernet0        |
|Switch           |Switch1      |ESW2-Fa1/2 ESW2-Fa1/3|Eth0 - Eth1      |
|Switch           |Switch2      |ESW3-Fa1/2 ESW3-Fa1/3|Eth0 - Eth1      |
|EtherSwitch      |ESW1         |R1-Fa0/0             |FastEthernet1/0  |
|EtherSwitch      |ESW2         |ESW1-Fa1/1 ESW1-Fa1/2|Fa1/4 - Fa1/5    |
|EtherSwitch      |ESW2         |ESW3-Fa1/0 ESW3-Fa1/1|Fa1/0 - Fa1/1    |
|EtherSwitch      |ESW3         |ESW1-Fa1/3 ESW1-Fa1/4|Fa1/4 - Fa1/5    |

*Nota:* Se realizo una configuracion portchannel en las conexiones entre los switch.


Las configuraciones del router (tanto la dirección de red como la dirección ip de cada subinterfaz como mascara de subred, etc), se detalla en la siguiente tabla:


|Interfaz           |Direccion IP   |
| ----------------  |-------------- |
|FastEthernet 0/0.15|192.168.15.254 |
|FastEthernet 0/0.25|192.168.25.254 |


En los host se implementaron las siguientes configuraciones:

|Tipo de Host     |Nombre       | Conectado a |Direccion IP  |
| --------------- | ----------- | ----------- |------------- |
|VPC              |PC1          |Switch1      |192.168.25.10 |
|VPC              |PC2          |Switch2      |192.168.15.11 |
|VPC              |PC3          |Switch2      |192.168.25.11 |
|Máquina Virtual  |TinyLinuxVM-1|Switch1      |192.168.15.10 |


Siendo la configuracion final la siguiente: 


|Tipo de Host     |Nombre       | Conectado a |Direccion IP  |Mascara de Red  |Gateway       |
| --------------- | ----------- | ----------- |------------- |--------------- |------------- |
|VPC              |PC1          |Switch1      |192.168.25.10 |255.255.255.0   |192.168.25.254|
|VPC              |PC2          |Switch2      |192.168.15.11 |255.255.255.0   |192.168.15.254|
|VPC              |PC3          |Switch2      |192.168.25.10 |255.255.255.0   |192.168.25.254|
|Máquina Virtual  |TinyLinuxVM-1|Switch1      |192.168.15.11 |255.255.255.0   |192.168.15.254|

#### Centro de Datos

Los datos y la forma en la que se implemetaron las Vlans esta dada de la siguiente forma:


|VLAN     |Direccion de Red  |Primera Direccion Asignable |Ultima Direccion Asignable  |Direccion de Broadcast|
| ------- | ---------------- | -------------------------- |--------------------------- | -------------------- |
|10       |192.168.15.0/24   |192.168.15.1                |192.168.15.254              |192.168.15.255        |
|20       |192.168.25.0/24   |192.168.25.1                |192.168.25.254              |192.168.25.255        |


Dando como resultado la topología de la siguiente forma:

![image](https://user-images.githubusercontent.com/37676214/95933938-eac08480-0d8c-11eb-823c-77e17c1c1038.png)



## Configuracion de los Equipos

### VPC

Colocar una VPC y posteriormente configurarla se realizan los siguiente pasos:

 1. Se toma selecciona una imagen de VPC entre los dispositivos. 
 2. Se arrastra el dispositivo al area de trabajo.
 3. Se enciende (Click derecho -> Start).
 4. Se entra a la terminal del dispositivo (Click derecho -> Console).
 
Una vez en el terminal del dispositivo se siguen los siguientes pasos.

 1. Se le asigna una dirección IP al dispositivo, con su respectiva mascara de subred. 
```sh
# ip [direccion/mascara gateway]
```
 2. Se salvan los cambios.
```sh
# save
``` 
 3. Opcionalmente se puede visualizar si la dirección ip.
```sh
# show ip
```

#### Configuración de PC1

Siguiendo el algoritmo anterior dispositivo PC1 se configuró de la siguiente forma.

-![image](https://user-images.githubusercontent.com/37676214/95934395-fbbdc580-0d8d-11eb-903f-3ddf38bd7673.png)

#### Configuración de PC2

Siguiendo el algoritmo anterior dispositivo PC2 se configuró de la siguiente forma.

-
![image](https://user-images.githubusercontent.com/37676214/95934424-08dab480-0d8e-11eb-9a9e-00316af679c5.png)
#### Configuración de PC3

Siguiendo el algoritmo anterior dispositivo PC3 se configuró de la siguiente forma.

-
![image](https://user-images.githubusercontent.com/37676214/95934478-23149280-0d8e-11eb-8074-c56960055ca1.png)

### Configuración de la maquina virtual.

Para configurar la maquina virtual se sigue el siguiente algoritmo. 

1. Se enciende el dispositivo (Click derecho -> Start).

Nota: Esta maquina virtual debe haber sido creada previamene en VMWare o en VirtualBox y haber sido importada a GNS3.

2. Una vez encendida la maquina virtual, vamos a su configuración.

3. Abrimos Panel de control.
-
![image](https://user-images.githubusercontent.com/37676214/90329539-efbab080-df62-11ea-8366-35f1ca94eed2.png)

4. Abrimos Network
-
![image](https://user-images.githubusercontent.com/37676214/90329552-0fea6f80-df63-11ea-84f8-9efe2cf8f57a.png)

5. Ingresamos la configuración correspondiente. 

6. Damos click donde dice aplicar. 
-
![image](https://user-images.githubusercontent.com/37676214/95934561-640ca700-0d8e-11eb-83da-3285c13a954e.png)

7. Cerramos.

8. Opcional
- Verificamos la configuración el siguiente comando la terminal.
```sh
$ ifconfig
``` 
-
![image](https://user-images.githubusercontent.com/37676214/95934587-75ee4a00-0d8e-11eb-95fa-4b685a2fb002.png)

### Configuración del Router


Para configurar el router, se sigue el siguente algoritmo.


1. Se arrasta el router al area de trabajo.
2. Se enciende (Click derecho -> Start).
3. Se entra al terminal (Click derecho -> console).
4. Se entra a modo privilegiado en el router.

```sh
R1 > enable
``` 

5. Opcionalmente podemos visualizar un resumen de la interfaz ip. 

```sh
R1# show ip interface brief
``` 
Obteniendo el siguiente resultado. 

-
![image](https://user-images.githubusercontent.com/37676214/91649603-f6512980-ea32-11ea-8526-85b01e25391c.png)

6. Procedemos a ingresar en la configuración del router.

```sh
R1# configure terminal
``` 

7. Configuramos la interfaz.

```sh
R1(config)# int fastethernet 0/0
``` 

8. Configuramos la velocidad de la interfaz.

```sh
R1(config-if)# speed auto 
``` 

9. Configuramos el modo full-duplex de la interfaz.

```sh
R1(config-if)# full-duplex
``` 

10. Encendemos la interfaz.

```sh
R1(config-if) # no shutdown
``` 

11. Salimos de la configuracion de la interfaz.

```sh
R1(config-if)# exit 
``` 
12. Ingresamos a la subinterfaz creandola

```sh
R1(config)#int fastethernet 0/0.15
```

13.Insertamos la dirección IP que tendrá esta subinterfaz.

```sh
R1(config-subif)# ip address 192.168.15.254 255.255.255.0
``` 

14. Encapsulamos la vlan que transitara por este puerto

```sh
R1(config-subif)# encapsulation dot1Q 10
```

15. Salimos

16. Repetimos del paso 12 al 15 con los siguientes valores
-Interfaz: FastEthernet 0/1 
-IP:       192.168.25.254
-Mascara:  255.255.255.0
-Vlan:     20

17. Salimos de la configuracion del Router

```sh
R1(config)# exit 
``` 

18. Guardamos los cambios.

```sh
R1# write memory 
``` 

19. Verificamos que la configuracion este bien.  

```sh
R1# show ip interface brief
``` 
Si todo esta bien el router deberia tener este resumen de interfaz ip. 

-
![image](https://user-images.githubusercontent.com/37676214/95937203-74c01b80-0d94-11eb-8905-128ec9ca73c4.png)


### Configuración de los EtherSwitch

#### Configuracion de puertos
Para configurar correctamente los switch ethernet seguimos el siguiente algoritmo.

1. Activamos el modo privilegiado.
```sh
ESW1>enable
```
2. Entramos a la configuracion del switch.
```sh
ESW1#configure terminal
```
3. Bajamos el Etherswitch a capa 2
```sh
ESW1(config)#no ip routing
```

4. Ponemos los puertos conectados a otro switch o router.

4.1. Entramos en las interfaces a configurar (puerto)
```sh
ESW1(config)#interface range fastethernet 1/0 - 5
```

4.2. Ponemos el puerto en modo trunk, configuramos en full-duplex y lo encendemos. 

```sh
ESW1(config-if-range)#switchport mode trunk
ESW1(config-if-range)#duplex full
ESW1(config-if-range)#no shutdown
```
5. Salimos y guardamos la configuracion
```sh
ESW1(config-if-range)#exit
ESW1(config)#exit
ESW1# write memory
```

6. Se repite el procedimiento para todos los EtherSwitch debiendo quedar de la siguiente forma.
-
![image](https://user-images.githubusercontent.com/37676214/95938149-81457380-0d96-11eb-8d4f-ebe54120c0fe.png)



#### Configuracion de VTP

Para configurar el VTP debemos definir cual de nuestros dispositivos sera el server que replicara las configuraciones de las Vlan a los demas dispositivos que en este caso seran clientes. 

Para esta practica el ESW1 sera el server y ESW2 Y ESW3 seran los clientes.

Para configurar el VTP en todos los casos se sigue el siguiente procedimiento, variando en el paso en el que se le asignara el rol. 

1. Entramos en la base de datos de la vlan.

```sh
ESW1# vlan database
```

2. Definimos el dominio del vtp
```sh
ESW1(vlan)# vtp domain redes1_201603095
```

3. Definimos el password del vtp 
```sh
ESW1(vlan)# vtp password redes1_201603095
```

4. Definimos el modo en el que trabajara el vtp
```sh
ESW1(vlan)# vtp v2-mode
```
5. En este paso variara dependiendo del ESW  que estemos configurando 

5.1. Se colocara el rol server al ESW1 

```sh
ESW1(vlan)# vtp server
```
5.2. Se colocara client en el ESW2 Y ESW3

```sh
ESW1(vlan)# vtp client
```

6. Finalmente la configuracion del VTP debe quedar de la siguiente forma:

6.1 ESW1.

-
![image](https://user-images.githubusercontent.com/37676214/95938780-d2a23280-0d97-11eb-8ac2-21619325730f.png)

6.2. ESW2 Y ESW3.

-
![image](https://user-images.githubusercontent.com/37676214/95938721-b2727380-0d97-11eb-822e-151279c92000.png)


#### Creacion de VLAN

Una vez configurado el vtp podemos crear las vlan para que automaticamente estas se repliquen del server a los demas etherswitch client, para hacer debemos ingresar los siguientes comandos;

1. Entramos a la configuracion
```sh 
ESW1#configure terminal
```
2. Creamos la vlan
```sh
ESW1(config)#vlan 10
```

3. Le damos nombre a esa vlan
```sh
ESW1(config-vlan)#name VENTAS
```
4. Repetimos el proceso con la vlan 20, nombre CONTABILIDAD.

5. Quedando la configuracion de las vlan de la siguiente forma en todos los ESW.

- 
![image](https://user-images.githubusercontent.com/37676214/95939383-30834a00-0d99-11eb-9077-2b1207978147.png)


#### Creacion de Portchannel

Para crear un portchannel debemos seguir la siguiente secuencia de comandos:

1. Entramos a la configuracion del equipo
```sh
ESW1#configure terminal
```
2. Seleccionamos las interfaces a añadir.
```sh
ESW1(config)#interface range fa 0/1 - 2 
```
3. Los añadimos a un numero de channel group y lo encendemos.
```sh
ESW1(config-if-range)#channel-group 1 mode on
```
4. Salimos y posteriormente verificamos que que este añadido.
```sh
ESW1(config-if-range)#exit
ESW1(config)#exit
ESW1#sh interface status
```
5. Esto se hace para las conexiones dobles de un ESW a otro.
-
![image](https://user-images.githubusercontent.com/37676214/95941343-cc16b980-0d9d-11eb-97f0-98d4dacf5073.png)

-
![image](https://user-images.githubusercontent.com/37676214/95941414-f7010d80-0d9d-11eb-9adb-5ecd3d66a424.png)

- 
![image](https://user-images.githubusercontent.com/37676214/95941467-1304af00-0d9e-11eb-9dfe-f510b7059d54.png)

#### Configuracion de STP

La configuracion del spanning tree protocol (STP) sera la configuracion por defecto para redes redundantes, para verificar la configuracion del mismo se utiliza el siguiente comando:

```sh 
ESW1# sh spanning-tree brief
```
Este comando se puede colocar en todos los dispositivos ESW para verificar cual de ellos es el root dentro del protocolo y asi mismo descubrir cual es el camino principal o que puertos estan bloqueados. 

El resumen de la configuracion de este protoco la los ESW es el siguiente:

-
![image](https://user-images.githubusercontent.com/37676214/95941795-d2596580-0d9e-11eb-8af9-938721271997.png)

-
![image](https://user-images.githubusercontent.com/37676214/95941835-eac98000-0d9e-11eb-93fc-db21f23085a2.png)

-
![image](https://user-images.githubusercontent.com/37676214/95941855-f9179c00-0d9e-11eb-956e-ca9e796c1424.png)

La topologia con el modo de los puertos asignados seria la siguiente:

-
![image](https://user-images.githubusercontent.com/37676214/95942145-a8547300-0d9f-11eb-8ea7-84e42dcdfb0a.png)


La ruta principal que tomarian los paquetes tomando en cuenta los puertos bloqueados seria la siguiente:

-
![image](https://user-images.githubusercontent.com/37676214/95942247-eea9d200-0d9f-11eb-90fa-b782b9de1791.png)


### Configuracion Switches

En GNS3 estos switch no se pueden configurar por medio de la consola, asi que la solucion es configurarlos a traves de su asistente. 

En este caso se deben de poner los puertos que van a los host (VPCs y Maquina virtual) en modo acceso al numero de vlan que pertenecen y los puertos que van a los ESW en modo trunk de la siguiente forma:

-
![image](https://user-images.githubusercontent.com/37676214/95943023-f0749500-0da1-11eb-9a47-a89829bd3dcc.png)

-
![image](https://user-images.githubusercontent.com/37676214/95943050-03876500-0da2-11eb-8e48-0b1edaf8e6fc.png)

### Captura de paquetes en la ruta principal y en la ruta bloqueada

-
![image](https://user-images.githubusercontent.com/37676214/95944341-3d0d9f80-0da5-11eb-9920-6dd85361a38a.png)


### Verificando Conexiones

Una vez, conectado y configurado de la forma anteriormente descrita, las configuraciones ya nos deberian permitir la comunicacion entre todas las maquinas, Esto se puede corroborrar haciendo ping desde la terminal de cualquier host hacia cualquiera de las direcciones ip de los demás. 

#### TinyLinuxVM-1

- ![image](https://user-images.githubusercontent.com/37676214/95942837-7512e380-0da1-11eb-9f5e-eeb324db188f.png)

#### PC1

- ![image](https://user-images.githubusercontent.com/37676214/95942613-d9817300-0da0-11eb-866d-3471ad87b785.png)


#### PC2

- ![image](https://user-images.githubusercontent.com/37676214/95942682-0df52f00-0da1-11eb-8ca7-7c0e831dfc98.png)

#### PC3

- ![image](https://user-images.githubusercontent.com/37676214/95942735-32e9a200-0da1-11eb-8ec8-d82c260b63f7.png)



