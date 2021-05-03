====== NVIDIA Optimus ======
**NOTAS**: 
  * //Dependiendo de tu tarjeta gráfica, tendrás que instalar una versión del driver diferente, puedes ver cuál te corresponde en: [[https://www.nvidia.es/Download/index.aspx?lang=es|NVIDIA Drivers]] Si es inferior a 340xx o 390xx no te vale este procedimiento.//
  * //Válido solo para X.org, esta configuración de NVIDIA Optimus no es válida para Wayland porque es otro servidor gráfico.//

  * Requisitos: 
    * Tener instalado los repositorios [[linux:fedora:guides:repos#rpm_fusion|RPM Fusion]]
    * Identificar la tarjeta gráfica (Procedimiento probado y certificado con el siguiente hardware):
      * Portátil Gigabyte Sabre 15
      * NVIDIA GeForce GTX 1050
      * Intel HD Graphics 630

  * Instalando:
<code bash>
sudo dnf install nvidia-settings nvidia-drivers acpi acpid gcc make binutils gcc-c++
</code>
  * Reiniciar el portátil
      * Si has instalado un kernel nuevo, a la hora de arrancar puede que tarde un poco, es porque está compilando el driver e instalándolo.
  * Identificar los diferentes proveedores de video:
<code bash>
xrandr --listproviders
</code>
  * Tendrá que haber salido una salida como esta:
<code bash>
Providers: number : 2
Provider 0: id: 0x1b8 cap: 0x1, Source Output crtcs: 4 outputs: 2 associated providers: 1 name:NVIDIA-0
Provider 1: id: 0x1e5 cap: 0xf, Source Output, Sink Output, Source Offload, Sink Offload crtcs: 3 outputs: 4 associated providers: 1 name:modesetting
</code>
      * Si ha cambiado ''NVIDIA-0'' por ''NVIDIA-G0'', no pasa nada.
  * Añadir la siguiente configuración de X.org ''/etc/X11/xorg.conf.d/10-nvidia-drm-outputclass.conf'' 
<code bash>
Section "OutputClass"
    Identifier "intel"
    MatchDriver "i915"
    Driver "modesetting"
EndSection

Section "OutputClass"
    Identifier "nvidia"
    MatchDriver "nvidia-drm"
    Driver "nvidia"
    Option "AllowEmptyInitialConfiguration"
    Option "PrimaryGPU" "yes"
    ModulePath "/usr/lib/nvidia/xorg"
    ModulePath "/usr/lib/xorg/modules"
EndSection
</code>
  * Asegurar que el módulo está cargado:
<code bash>
lsmod |grep nvidia
</code>
    * Tendrá que haber salido una cosa como esta:
<code bash>
nvidia_drm             61440  13
nvidia_modeset       1220608  33 nvidia_drm
nvidia_uvm           1150976  0
nvidia              28286976  2124 nvidia_uvm,nvidia_modeset
drm_kms_helper        266240  2 nvidia_drm,i915
drm                   626688  16 drm_kms_helper,nvidia_drm,i915
</code>
===== Configurar LightDM =====
  * Editar el archivo: ''/etc/lightdm/display_setup.sh''
    * ''NVIDIA-0'', si tiene otro nombre, cambiarlo en el script.
<code bash>
#!/bin/sh
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
</code>
  * Asignar permisos de ejecución 
<code bash>
sudo chmod +x /etc/lightdm/display_setup.sh
</code>
  * Modificar ''/etc/lightdm/lightdm.conf''
<code bash>
[Seat:*]
display-setup-script=/etc/lightdm/display_setup.sh
</code>
  * Reiniciamos el interfaz gráfico
<code bash>
sudo systemctl isolate multi-user.target
sudo systemctl isolate graphical.target
</code>
===== Configurar SDDM (Plasma Login) =====
  * Editar el archivo: ''/etc/sddm/Xsetup''
    * ''NVIDIA-0'', si tiene otro nombre, cambiarlo en el script.
<code bash>
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
</code>
  * Reiniciamos el interfaz gráfico
<code bash>
sudo systemctl isolate multi-user.target
sudo systemctl isolate graphical.target
</code>

Si no usamos un GDM
  * Crear o editar este archivo ''~/.xinitrc''
    * ''NVIDIA-0'', si tiene otro nombre, cambiarlo en el script.
<code bash>
~/.xinitrc
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
</code>
  * Lanzar el interfaz ''startx''
    * **NOTA**: //Si no tienes un gestor de entrada o entorno de escritorio no te funcionará a menos que tengas ''twm'' instalado, si no tendrás que configurar el entorno/gestor de ventanas que utilices con la sentencia ''exec blabla''//

==== Fuentes ====
  * [[https://wiki.archlinux.org/index.php/NVIDIA_Optimus|Guía basada en la instalación de NVIDIA Optimus - ArchWiki]]

