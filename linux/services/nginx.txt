====== Introducción ======

====== Server Blocks ======
Para crear un server block, lo equivalente a un virtual host en Apache, utilizamos la siguiente sintaxis:
Creamos un archivo en ''/etc/nginx/conf.d/serverblock.conf'''

<code bash>
server {
  listen 80;
  server_name localhost;
  
}
</code>

