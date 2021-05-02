====== Introducción ======
''kdump'' es un servicio que permite volcar una falla del kernel para después analizarla.

====== Instalando ======
  * Instalar el paquete ''kexec-tools''
<code bash>
sudo dnf install kexec-tools
</code>

====== Configurando el gestor de arranque ======
  * Editamos ''/etc/default/grub'' y añadimos este parámetro dentro de ''GRUB_CMDLINE_LINUX=''
<code bash>
crashkernel=128M
</code>
  * Reconfiguramos el grub en el caso de no usar UEFI
<code bash>
sudo grub2-mkconfig -o /boot/grub.cfg
</code>
  * Si usamos UEFI
<code bash>
sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
</code>
====== systemd ======

  * Habilitamos el servicio al arranque:
<code bash>
sudo systemctl enable kdump.service
</code>

====== Reiniciamos y comprobamos ======

  * Una vez que inicie la máquina, comprobamos que está levantado el servicio:
<code bash>
sudo systemctl status kdump.service

● kdump.service - Crash recovery kernel arming
     Loaded: loaded (/usr/lib/systemd/system/kdump.service; enabled; vendor preset: disabled)
     Active: active (exited) since Mon 2021-01-11 19:26:15 CET; 6min ago
    Process: 1587 ExecStart=/usr/bin/kdumpctl start (code=exited, status=0/SUCCESS)
   Main PID: 1587 (code=exited, status=0/SUCCESS)
        CPU: 21.331s
Jan 11 19:26:15 shark0 kdumpctl[1589]: kdump: kexec: loaded kdump kernel
Jan 11 19:26:15 shark0 kdumpctl[1589]: kdump: Starting kdump: [OK]
Jan 11 19:26:15 shark0 systemd[1]: Finished Crash recovery kernel arming.
</code>

====== Recursos ======
[[https://docs.fedoraproject.org/en-US/Fedora/17/html/System_Administrators_Guide/s2-kdump-configuration-cli.html|Fedora Docs]]
