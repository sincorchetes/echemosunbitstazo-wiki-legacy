====== Instalar paquete de codificación/idioma ======
  * Si has instalado la edición de Fedora en inglés, pero quieres soportar otras codificaciones/locales.
<code bash>
sudo dnf install glibc-langpack-ny
</code>
  * ''ny'' representa las dos letras del idioma, es por ejemplo para el español.

====== Cambiar la codificación/idioma del sistema ======
  * Ver la configuración actual:
<code bash>
localectl status 
</code>
  * Listar las opciones disponibles
<code bash>
localectl list-locales
</code>
  * Configurar
<code bash>
sudo localectl set-locale aa_bb.codificación
</code>
  * Mostrar los idiomas de teclado tanto para X11 (X.org) y para tty o modo consola
<code bash>
localectl list-keymaps
</code>
  * Configurar un idioma de teclado tanto para X11 (X.org) y para tty o modo consola
<code bash>
localectl set-keymap
</code>
  * Reiniciar el sistema

====== Páginas de documentación, man ======

===== Instalar traducciones =====
NOTA: Es necesario tener la codificación 
  * Buscar traducciones disponibles:
<code bash>
sudo dnf search man-pages
</code>

  * Instalar la traducción, por ejemplo español:
<code bash>
sudo dnf install man-pages-es man-pages-es-extra
</code>

===== Realizar consultas en otros idiomas =====
  * Bastará con ejecutar el siguiente comando:
<code bash>
man -L es man
</code>

====== Libreoffice ======
===== Idioma de interfaz =====
  * Para buscar los idiomas de interfaz disponibles
<code bash>
sudo dnf search libreoffice-langpack
</code>
  * Para instalarlo, por ejemplo, el español:
<code bash>
sudo dnf install libreoffice-langpack-es
</code>
NOTA: Este detectará tambień el idioma que falta en el entorno de escritorio y el corrector ortográfico (Hunspell) utilizado por el proyecto.

====== Plasma (KDE) ======
  * Para ver los idiomas disponibles:
<code bash>
sudo dnf search kde-l10n
</code>

  * Instalar el soporte idiomático en español:
<code bash>
sudo dnf install kde-l10n-es
</code>
