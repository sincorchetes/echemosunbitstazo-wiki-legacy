====== Docker ======
  * Instalar algunos componentes necesarios e instalar Docker
<code bash>
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io
sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"
</code>
  * Reiniciar el equipo
  * Habilitar y arrancar el servicio al arranque
<code bash>
sudo systemctl enable --now docker.service
</code>

===== Ejecutar Docker sin necesitar privilegios =====
  * Añadir el usuario que necesites al grupo ''docker''
<code bash>
sudo gpasswd -a USUARIO docker
</code>
  * Salir y entrar de la sesión o ejecutar:
<code bash>
newgrp docker
</code>

===== Instalar Docker Compose =====
  * Ejecutar la siguiente instrucción:
<code bash>
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
</code>
  * Para realizar cualquier operativa basta con que ejecutes ''docker-compose''

Para más información de cómo utilizar este servicio, sigue esta página.

====== Fuentes ======
  * [[https://docs.docker.com/engine/install/fedora/|Instalación (doc oficial - Docker]]
  * [[https://docs.docker.com/engine/install/linux-postinstall/|Post instalación (doc oficial)- Docker]]
  * [[https://docs.docker.com/compose/install/|Instalación Docker Compose (doc oficial)]]

