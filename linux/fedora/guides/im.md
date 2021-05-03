====== Mensajería instantánea ======
===== Telegram Desktop =====
  * Requisitos previos:
    * Tener habilitado los repositorios [[linux:fedora:guides:repos#rpm_fusion|RPM Fusion]]
  * Instalando:
<code bash>
sudo dnf install telegram-desktop
</code>
  * Bastará con ejecutar ''telegram-desktop''

====== Herramientas de colaboración en línea ======

===== Slack =====
NOTA: Puede variar la versión, si hay un error 404 puedes descargarla desde esta [[https://slack.com/intl/en-es/downloads/instructions/fedora|página]].
  * Instalar:
<code bash>
curl -LO https://downloads.slack-edge.com/linux_releases/slack-4.12.0-0.1.fc21.x86_64.rpm
sudo dnf install slack-4*.rpm
</code>
  * Basta con ejecutar ''slack''
