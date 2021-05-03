====== Códecs audio/video ======
  * Requisitos: 
    * Tener instalado los repositorios [[linux:fedora:guides:repos#rpm_fusion|RPM Fusion]]
  * Instalando:
<code bash>
sudo dnf install gstreamer-plugins-ugly.x86_64 gstreamer1-plugins-bad-free-extras.x86_64 \
gstreamer1-plugins-good-extras.x86_64 gstreamer1-vaapi.x86_64 
sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf groupupdate sound-and-video
</code>

====== Reproductores de audio ======
===== Clementine =====
  * Instalación:
<code bash>
sudo dnf install clementine
</code>
  * Basta con lanzar ''clementine''
===== Spotify =====
  * Requisitos: 
    * Tener instalado los repositorios [[linux:fedora:guias:repos|RPM Fusion]]

  * Instalando:
<code bash>
sudo dnf install lpf-spotify-client
lpf-gui
</code>
  * Seguir los pasos y ya lo tendrías instalado, para ejecutarlo: ''spotify''

====== Videoconferencia ======

===== Skype =====
  * Ejecutar:
<code bash>
curl -LO https://go.skype.com/skypeforlinux-64.rpm
sudo dnf install skypeforlinux-64.rpm
</code>

  * Para lanzarlo, ejecuta ''skypeforlinux''


===== Zoom =====
  * Ejecutar:
<code bash>
curl -LO https://zoom.us/client/latest/zoom_x86_64.rpm
sudo dnf install zoom_x86_64.rpm
</code>

  * Para lanzarlo, basta con ejecutar: ''zoom''



====== Fuentes ======
  * [[https://rpmfusion.org/Configuration|Códecs - Basada en la wiki de RPM Fusion]]
