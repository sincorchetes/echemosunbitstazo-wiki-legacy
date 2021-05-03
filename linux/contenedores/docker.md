====== Docker ======

===== Gestión de contenedores =====

==== Lanzar ===
  * Lanzar un contenedor NGINX en modo segundo plano y que se ejecute en el puerto 80
<code bash>
sudo docker run -d -p 80:80 nginx
</code>
  * Lanzar un contenedor NGINX en modo segundo plano y que se ejecute en el puerto 8080
<code bash>
sudo docker run -d -p 8080:80 nginx:latest
</code>

  * Lanzar un contenedor con un nombre identificativo
<code bash>
sudo docker run -d -n NGINX -p 80:80 nginx:latest
</code>
  * Lanzar un contenedor para ejecutar cosas en él
<code bash>
sudo docker run -ti centos:latest /bin/bash
</code>
  * Mapear una unidad del SO en un contenedor
<code bash>
sudo docker run -ti -v /home/sincorchetes:/app centos:latest /bin/bash
</code>

==== Listar ====
  * Listar los contenedores incluyendo los que no están en marcha
<code bash>
sudo docker ps -a
</code>

  * Listar los contenedores que solo están en marcha
<code bash>
sudo docker ps
</code>

==== Operaciones de eliminado ====
  * Eliminar todos los contenedores incluyendo los que están en marcha, dieron error o no se han desplegado
<code bash>
sudo docker rm -f $(docker ps -a | awk '{print $1}' | tail -n +2)
</code>

  * Eliminar todos los contenedores solo lo que están en marcha
<code bash>
sudo docker rm -f $(docker ps | awk '{print $1}' | tail -n +2)
</code>


