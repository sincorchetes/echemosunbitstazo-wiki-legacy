====== Selenium ======
===== Google Chrome y Python =====

  * Requisitos:
    * Tener instalado Google Chrome
    * Tener instalado el plugin de [[https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd|Selenium IDE]]
    * Realizar una grabación o acciones en una página
    * Exportar el .side a .py desde el plugin de Chrome
<code bash>
sudo dnf install chromedriver
</code>
  * Crear ''Virtualenv''
<code bash>
python -m venv selenium
</code>
  * Instalar dependencias
<code bash>
source selenium/bin/active
pip install selenium pytest
</code>
  * Editar el archivo exportado ''*.py''
  * Añadir lo siguiente:
<code python>
  o = CLASE()
  o.setup_method('get')
  o.METODO()
</code>
  * Hay que cambiar CLASE y METODO según lo que hay en el archivo
  * Ejecutar el script
<code bash>
python NombreArchivo.py
</code>
