====== Virtualización ======

===== QEMU-KVM =====

==== Instalación ====
Para instalar el software solo necesitaremos instalar los siguientes paquetes:
<code bash>
sudo dnf install -y qemu-kvm
</code>

=== Crear unidades de almacenamiento ===
  * QCOW
<code bash>

</code>

==== Utilidades gráficas ====
  * [[linux:fedora:guides:virt:virt-manager|virt-manager]]

===== VirtualBox =====
  * Requisitos: 
    * Tener instalado los repositorios [[linux:fedora:guides:repos|RPM Fusion]]
  * Instalando:
<code bash>
sudo dnf install VirtualBox elfutils-libelf
</code>
  * Añadir el usuario que lo va a utilizar
<code bash>
sudo gpasswd -a USUARIO vboxusers
</code>
  * Salir y entrar de la sesión

==== Bonus extra: Instalar VirtualBox Extension pack ====
**NOTA**: Permiten usar puertos 3.0 como tal entre otras cosas.
  * Instalar:
<code bash>
curl -LO https://download.virtualbox.org/virtualbox/6.1.16/Oracle_VM_VirtualBox_Extension_Pack-6.1.16.vbox-extpack
xdg-open Oracle_VM_VirtualBox_Extension_Pack-6.1.16.vbox-extpack
</code>
  * Seguir los pasos y listo.