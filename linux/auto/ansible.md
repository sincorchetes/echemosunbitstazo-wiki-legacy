====== Ansible ======
===== Playbooks =====
  * Crear un playbook que muestre la fecha/hora del sistema:
<code yaml>
---
- name: Obtener fecha/hora
  hosts: {{ host }}

  tasks:
  - name: Obtener fehca/hora del sistema
    shell: date
</code>

