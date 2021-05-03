====== Introducción ======
Cuando Fedora se instala hay servicios que podemos prescindir de ellos o deshabilitarlos si no los utilizamos, así evitamos problemas de seguridad y reduciremos en consumo, a pesar de que puede que el sistema  no se inicie con todos los servicios que he expuesto aquí, es recomendable desactivar los que no necesitemos.

===== fprintd - Lector de huellas =====
Si no utilizamos un lector de huellas, es mejor deshabilitarlo
<code bash>
sudo systemctl disable --now fprintd.service
</code>

===== livesys/livesys-late - Servicios LiveCD/DVD/USB =====
Estos servicios se utilizan para configuraciones mientras se instala la distribución pero no nos hace más falta una vez instalada
<code bash>
sudo systemctl disable --now livesys
sudo systemctl disable --now livesys-late
</code>

===== Bluetooth - Sistema de conexion PAN =====
Si no tienes un dispositivo de Bluetooth o lo quieres utilizar solo bajo demanda, conviene desactivarlo y activarlo cuando guste.
<code bash>
sudo systemctl disable --now bluetooth.service
sudo systemctl disable --now bluetooth.target
</code>

===== Avahi - Autodescubrimiento =====
Si no utilizas autodescubrimiento en la red local, no hace falta que los tengas
<code bash>
sudo systemctl disable --now avahi-daemon.service
sudo systemctl disable --now avahi-daemon.socket
</code>
===== CUPS - Impresoras =====
Si no tienes impresoras, ¿para qué lo necesitas?
<code bash>
sudo systemctl disable --now cups.service
</code>

===== NFS - Sistema de archivos en red =====
Si no usas NFS cliente/servidor, desactívalo:
<code bash>
sudo systemctl disable --now nfs-blkmap.service
sudo systemctl disable --now nfs-client.target
sudo systemctl disable --now nfs-server.service
sudo systemctl disable --now nfs-convert.service
</code>

===== scsi - Sistemas de detección y manipulación SCSI =====
Si solo usas pendrives, discos SATA/IDE, SSD... no hace falta tener este servicio
<code bash>
sudo systemctl disable --now iscsid.service
sudo systemctl disable --now iscsid.socket
sudo systemctl disable --now iscsi.service
sudo systemctl disable --now iscsiuio.service
sudo systemctl disable --now iscsiuio.socket   
</code>

===== RAID - Sistema de replicación de discos/disp almacenamiento =====
Si no lo usamos
<code bash>
sudo systemctl disable raid-check.timer
</code>

===== LVM - Gestor de Volúmenes de Linux =====
  * **NOTA**:** DESACTIVAR SOLO SI NO USAMOS LVM O PROVOCARÁ UN SISTEMA INSERVIBLE**
<code bash>
sudo systemctl disable lvm2-lvmpolld.socket
sudo systemctl disable lvm2-monitor.service
</code>