====== FirewallD ======

  * Habilitar un puerto específico TCP de forma temporal
<code bash>
firewall-cmd --add-port XXX/tcp
</code>

  * Habilitar un puerto específico TCP de forma permanente
<code bash>
firewall-cmd --add-port XXX/tcp --permanent
firewall-cmd --reload
</code>

  * Habilitar un puerto específico UDP de forma temporal
<code bash>
firewall-cmd --add-port XXX/udp
</code>

  * Habilitar un puerto específico UDP de forma permanente
<code bash>
firewall-cmd --add-port XXX/udp --permanent
firewall-cmd --reload
</code>