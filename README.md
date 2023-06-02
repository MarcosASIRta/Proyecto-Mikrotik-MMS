# Configuración de dispositivos Mikrotik

Paso a paso de la configuración de dos dispositivos Mikrotik (hAP y hEX).

## Descripción

En este proyecto haremos una instalación con dispositivos Mikrotik creando varias redes incluyendo una Wifi. En este caso, haremos 4 redes de las cuales una será inalámbrica, otra conectará ambos routers y las otras dos serán una de cada router a través de cables ethernet (exeptuando dos interfaces, la 5 de cada router, que mantendremos sin modificar para que no surjan problemas a la hora de conectarnos para configurar dichos routers).

## Materiales

* 3 cables Ethernet.
* hAP Mikrotik.
* hEX Mikrotik.
* PC para configurar.
* Dispositivo móvil para realizar comprobaciones.

## Instalación física

* El dispositivo hEX se conecta, desde la interfaz de Internet, directamente a la red local del insitituto mediante un cable Ethernet directo al switch del aula que a su vez se conecta con el router de esta.
* El dispositivo hAP se conecta a la interfaz 2 del dispositivo hEX desde la interfaz de Internet mediante un cable Ethernet.
* El PC se conectará a la interfaz 5 de ambos dispotivos a medida que lo requeriramos para configurarlos.

## Configuración

Para configurar, accederemos a la interfaz 5 de cada router con un cable Ethernet desde el PC.

### hEX

* Empezaremos configurando la interfaz 2 creando un bridge nuevo para esta. Este bridge tendrá el nombre "bridge3".
* De paso, creamos otro bridge llamado "bridge2" y se lo asignaremos a las interfaces 3 y 4.
* Configuraremos estos bridges asignándoles puertas de enlace. El bridge 2 tendrá la puerta de enlance 192.168.10.1/24 y el bridge 3 tendrá la 192.168.0.1/24.
* Configuraremos ahora DHCP para el bridge 2. Para ello creamos un pool con el rango 192.168.10.10-192.168.10.50.
* Una vez creado el pool, creamos el servidor DHCP donde le asignaremos el bridge 2, el pool creado anteriormente y le ponemos como DNS el 8.8.8.8 y como puerta de enlace la 192.168.10.1.
* Con esto, ya habremos acabado la configuración del hEX.

###hAP

* Empezaremos configurando la interfaz de Internet asignandole la ip 192.168.0.2/24.
* A continuación, crearemos dos bridges siendo uno "wifi", el cual contendrá las interfaces Wlan5 y Wlan6, y el otro "bridge2" el cual tendrá las interfaces 2, 3 y 4.
* Le asignaremos puertas de enlace, al "wifi" la 192.168.50.1/24 y al "bridge2" la 192.168.40.1/24.
* Creamos dos pools para hacer dos servidores DHCP. Un pool será el de la Wifi, con el rango 192.168.50.10-192.168.50.50, y el otro será del bridge 2, con el rango 192.168.40.10-192.168.40.50.
* Unas vez creados los pools, creamos los servidores DHCP y le asignamos sus respectivas puertas de enlace y el DNS 8.8.8.8.
* Para la red Wireless, cambiaremos el nombre de la interfaz Wlan5 a Mikrotik-Marcos y la Wlan6 a Mikrotik-Marcos5G.
* Cambiamos estas interfaces a abridge y les asignamos el método de seguridad default al cual le cambiaremos la contraseña a "12345678".
* Con esto, finaliza la configuración del hAP.
