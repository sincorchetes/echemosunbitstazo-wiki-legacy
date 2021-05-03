====== Concepto ======
Los Playbooks permiten escribir guiones que permiten automatizar multitud de procesos y tareas sin tener que ir ejecutando cada uno de los comandos en modo ad-hoc en el resto de servidores.

====== Formato ======
Los playbooks utilizan un lenguaje de datos serializado llamado YAML.

====== Módulos ======
Son librerías desarrolladas para facilitar la gestión de determinadas tareas como la decompresión/compresión de archivos; cambios de permisos; gestión de paquetería...etc

====== Apuntes ======
===== Concatenar cadena con un valor de una variable =====
  * <code yaml>"{{ '.'.join(('www',dominio))}}"</code>

===== DNF =====
  * Actualizar todos los paquetes
<code yaml>
---
- name: Actualizar paquetería 
  hosts: "{{ host }}"

  tasks:
  - name: Actualizando la paquetería del sistema
    dnf:
      name: "*"
      state: latest
</code>