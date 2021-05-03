====== Python ======
CentOS 8 por defecto no tiene una versión de Python definida por defecto, para definirla, utilizamos el siguiente comando:
<code bash>
sudo alternatives --config python
</code>
Y nos saldrá una salida interactiva parecida a esta:
<code bash>
There are 3 programs which provide 'python'.

  Selection    Command
-----------------------------------------------
*+ 1           /usr/libexec/no-python
   2           /usr/bin/python3
   3           /usr/bin/python3.8

Enter to keep the current selection[+], or type selection number: N
</code>
Escribimos el número en el que estamos interesados utilizar y pulsamos Enter.

Si comprobamos la versión:
<code bash>
python -V
Python 3.8.3
</code>

===== ¿Cómo habilitar otras versiones de Python? =====
Ejecutamos el siguiente comando:
<code bash>
sudo dnf module list |grep python | grep -vE "selinux"
python27             2.7 [d]      common [d]                               Python programming language, version 2.7
python36             3.6 [d]      build, common [d]                        Python programming language, version 3.6
python38             3.8 [d][e]   build, common [d]                        Python programming language, version 3.8
python38-devel       3.8                                                   Python programming language, version 3.8
</code>

Para instalarla, por ejemplo, la versión 38:
<code bash>
sudo dnf module enable python38
sudo dnf install python38
sudo alternatives --config python
</code>
