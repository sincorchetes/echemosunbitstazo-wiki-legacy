====== Network Manager ======
===== Visualizando =====
  * Ver la configuración de una conexión
<code bash>
nmcli con show ens192
</code>
  * Ver un resumen de las conexiones
<code bash>
nmcli con
</code>

===== Creando una conexión =====
  * Tener previamente la IP que queremos configurar con su puerta de enlace y máscara de red
  * Saber cómo llamar la conexión y qué interfaz de red vamos a utilizar para esta conexión
<code bash>
sudo nmcli add type ethernet con-name NOMBRE_CONEXION ifname NOMBRE_INTERFAZ ip4 IP4/PERFIJO gw4 IP4_GATEWAY/PREFIJO ipv4.dns "X.X.X.X Y.Y.Y.Y"
</code>

===== Gestionando una conexión =====
  * Obtener listado de conexiones ''nmcli con''
<code bash>
nmcli con
</code>
  * Cambiar la IP y el gateway de una conexión
<code bash>
sudo nmcli con mod ens192 ip4 192.168.1.1 gw4 192.168.1.254
sudo nmcli con down ens192
sudo nmcli con up ens192
ip addr |grep ens192
</code>
===== Troubleshooting =====
==== Caso 1: La red nos dice que la IP se está utilizando pero si hacemos ping a la IP, esta no resuelve. ====
Tenemos una máquina virtual que accede a una red en modo bridge con la siguiente configuración:
  * IP de host:192.168.1.2 
  * Máscara de red: 255.255.255.0
  * Puerta de enlace: 192.168.1.1

Y cuando tratamos de levantar la interfaz, esta falla. Veamos la configuración y el procedimiento para levantar la interfaz con nuestra configuración:

Configuración en ''/etc/sysconfig/network-scripts/ifcfg-eth0'':
<code bash>
DEVICE=eth0
HWADDR=AB:CD:EF:GH:IJ:KL
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=no
BOOTPROTO=static
IPADDR=192.168.1.2
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
</code>

Tratando de levantar la interfaz:
<code bash>
# ifup eth0
Determining if ip address 192.168.1.2 is already in use for device eth0...
Error some other host already uses address 192.168.1.2.
</code>

Para diagnosticar si es cierto, utilizamos el comando arping:
<code bash>
# arping -c N -w N -D -I Nombre_Nic Dirección_IP
</code>
  * ''-c N'': Cuenta los paquetes que se envían
  * ''-w N'': Cuanto se tarda en obtener una respuesta
  * ''-D'': Duplica la dirección en modo de detención
  * ''-I Nombre_Nic'': Aquí definimos con qué interfaz de red realizar la prueba
  * Dirección_IP

<code bash>
# arping -c 2 -w 3 -D -I eth0 192.168.1.2
ARPING 192.1.68.1.2 from 0.0.0.0 eth0
Unicast reply from 192.168.1.2 [UU:VV:WW:XX:YY:ZZ] 0.926ms
</code>

Ahí tenemos una interfaz de un equipo X que está cogiendo esa IP.