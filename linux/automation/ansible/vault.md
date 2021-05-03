====== Encriptar datos ======
Ansible Vault es una funcionalidad que permite encriptar contraseñas en archivos.

===== Crear vault =====
<code bash>
ansible-vault create nombre_archivo
</code>

===== Editar información =====
<code bash>
ansible-vault edit 
</code>

<code bash>
# create vault file
ansible-vault create --encrypt-vault-id=foo foo_vault_file.yml

# edit the file in text editor
ansible-vault edit --encrypt-vault-id=foo foo_vault_file.yml

# in text editor, add variables and values of the form
# my_variable: my_value
# save the file

# use the vars file in a playbook
# this file is named test_vault_file.yml
---

- name: test encrypted vault file
  hosts: localhost
  connection: local
  vars_files:
    - foo_vault_file.yml
  tasks:
    - name: debug secret
      debug:
        var: my_variable

# output
$ ansible-playbook test_vault_file.yml

PLAY [test encrypted vault file] ************************************************************************************************************************************

TASK [debug secret] *************************************************************************************************************************************************
Wednesday 27 January 2021  06:58:02 -0600 (0:00:00.121)       0:00:00.121 ***** 
Wednesday 27 January 2021  06:58:02 -0600 (0:00:00.120)       0:00:00.120 ***** 
ok: [localhost] => 
  my_secret_value: thisissosecret

PLAY RECAP **********************************************************************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
</code>