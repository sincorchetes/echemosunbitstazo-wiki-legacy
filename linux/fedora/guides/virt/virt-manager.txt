====== Instalación ======
  * Instalando el paquete
<code bash>
sudo dnf install virt-manager
</code>

  * Levantando el servicio de ''libvirtd'' y asignandolo para que arranque al inicio del sistema
<code bash>
sudo systemctl enable --now libvirtd
</code>

====== Post-configuración ======

===== Usuario sin privilegios =====

  * Añadir usuario sin privilegios para que pueda ejecutar máquinas virtual
<code bash>
sudo gpasswd -a USUARIO libvirt
</code>

===== Lanzar el programa =====

  * Iniciarlo
<code bash>
virt-manager
</code>

