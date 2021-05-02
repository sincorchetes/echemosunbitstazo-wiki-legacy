====== systemd ======
  * [[linux:services:systemd:build_a_service|Creando un servicio]]

===== Configuración =====

==== Codificación del sistema ====
  * Obtener un resumen de la codificación del sistema:
<code bash>
localectl
</code>
  * Obtener un listado de las codificaciones disponibles:
<code bash>
localectl list-locales
</code>
  * Configurar una codificación del sistema:
<code bash>
sudo localectl set-locale en_US.utf8
</code>
==== Huso horario ====
  * Obtener un resumen de la fecha-hora del sistema:
<code bash>
timedatectl
</code>
  * Obtener lista de husos horarios
<code bash>
timedatectl list-timezones
</code>
  * Configurar huso horario
<code bash>
sudo timedatectl set-timezone Atlantic/Canary
</code>

==== Hostname ====
Para configurar el hostname de la máquina solo basta con ejecutar:
<code bash>
sudo hostnamectl set-hostname NOMBRE_MAQUINA
</code>

===== Troubleshooting =====
==== No encuentro la codificación que quiero ====
=== Fedora/CentOS/RHEL ===

Revisar los locales instalados
<code bash>
rpm -qa |grep glibc-langpack
dnf list installed langpacks*
</code>

Instalar el idioma específico
<code bash>
sudo dnf install glibc-langpack-IDIOMA
</code>

==== La pantalla del portátil entra en suspensión con AC y conectada a otro monitor ====

''/etc/systemd/logind.conf''
<code bash>
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
</code>

Reiniciar el servicio (no hacer SIGHUP como dice):
<code bash>
# systemctl restart systemd-logind
</code>

https://unix.stackexchange.com/questions/597360/how-to-disable-suspending-the-system-when-the-lid-is-closed
