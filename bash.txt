====== Bash ======
====== Archivos comprimidos ======
===== tar =====

  * Descomprimir un archivo ''.tar.gz''
<code bash>
tar xfv archivo.tar.gz
</code>

  * Ver dentro del archivo
<code bash>
tar jvf archivo.tar.gz
</code>

===== Gzip =====
  * Descomprimir un archivo
<code bash>
gzip -d archivo.gz
</code>
  * Listar contenido del archivo
<code bash>
gzip --list archivo.gz
</code>
  * Comprimir archivo
<code bash>
gzip archivo
</code>

====== Trabajos en segundo/primer plano ======

  * Crear un timeout para scripts/programas ejecutados en foreground
<code bash>
timeout --foreground 1 sh -c "comando"
</code>