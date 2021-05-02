====== Software a terceros ======
===== RPM Fusion =====

  * Instalar repositorios ''free'', ''non-free''
<code bash>
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf check-update
</code>

==== Fuentes ====
  * [[https://rpmfusion.org/Configuration|Instalación RPM Fusion - RPM Fusion]]