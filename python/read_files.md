====== Leer archivos ======

===== Discriminación log vsftpd =====

<code python>
#!/usr/bin/env python3
# Escrito por Álvaro Castillo Martín
#
import sys,os
logs_dir = os.getcwd()
vsftpd_logs = os.listdir(logs_dir)
users = {}

with open("usuarios_ftp") as f:
  users = f.read().rstrip("\n").split("\n")

for files in vsftpd_logs:
  with open(files,"r") as f:
    for line in f:
      if "230 Login" in line:
       for user in users:
         count_conn = 0
         if user in line:
            #print(user + line)
           coun_conn += 1
           print(coun_conn)
         else:
           coun_conn = 0
      elif "221 Goodbye" in line:
       for user in users:
         if user in line:
            print(user + line)
      else:
        pass

</code>
