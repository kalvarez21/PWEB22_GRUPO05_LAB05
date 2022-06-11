<table>
  <tbody>
   <tr>
   <td><img src="./imagenes/epis.png" alt="EPIS"></td>
   <th>
   <p>UNIVERSIDAD NACIONAL DE SAN AGUSTIN</p>
   <p>FACULTAD DE INGENIERÍA DE PRODUCCIÓN Y SERVICIOS</p>
   <p>ESCUELA PROFESIONAL DE INGENIERÍA DE SISTEMAS</p>
   </th>
   <td><img src="./imagenes/abet.png" alt="ABET"></td>
   </tr>
  </tbody>
</table>
<div align="center" dir="auto"><table>    
   <tbody>
   <tr><td colspan="3">Formato: Guía de Práctica de Laboratorio / Talleres / Centros de Simulación</td></tr>
   <tr><td>Aprobación:  2022/03/01</td><td>Código: GUIA-PRLD-001</td><td>Página: 1</td></tr>
   </tbody>
</table></div>
<div align="center" dir="auto">
   <span>INFORME DE LABORATORIO</span><br>
   <span>(formato estudiante)</span>
</div>
<div align="center" dir="auto"><table>
   <tbody><tr><th colspan="6">INFORMACIÓN BÁSICA</th></tr>
   </tbody><tbody>
   <tr><td>ASIGNATURA:</td><td colspan="5">Programación Web 2</td></tr>
   <tr><td>TÍTULO DE LA PRÁCTICA: </td><td colspan="5">Django</td></tr>
   <tr>
   <td>NÚMERO DE PRÁCTICA:</td><td>05</td><td>AÑO LECTIVO:</td><td>2022 A</td><td>NRO. SEMESTRE:</td><td>III</td>
   </tr>
   <tr>
   <td>FECHA Presentacion:</td><td>12-Jun-2022</td><td>Hora de Presentacion:</td><td colspan="3">23:55</td>
   </tr>
   <tr><td colspan="3">Integrantes:
   <ul dir="auto">
   <li>Kevin Jheeremy Alvarez Astete</li>
   </ul>
   </td>
   <td> NOTA: </td>
   <td colspan="2"> </td>
   </tr><tr><td colspan="6">DOCENTES:
   <ul dir="auto">
   <li>Richart Smith Escobedo Quispe (rescobedoq@unsa.edu.pe)</li>
   </ul>
   </td>
</tr></tbody></table></div>
   <h1>SOLUCION Y RESULTADOS</h1>
   <h2>I. SOLUCION DE EJERCICIOS/PROBLEMAS</h2>

   - Creacion del Blog - Paso a Paso:
   - Se inicia creando un entorno virtual:
   ```sh
    python -m venv myvenv
   ```

   - Inicializamos el entorno:
   ```sh
    myvenv/Scripts/activate.bat
   ```

   - Se crea un archivo requiremets.txt con cuyo contenido sera:
   ```sh
    Django~=3.2.10
   ```

   - Se procede a instalar Django:
   ```sh
    pip install -r requirements.txt
   ```

   - OPCIONAL: Si se desea actualizar pip se puede usar:
   ```sh
    python -m pip install --upgrade pip
   ```

   - Se crea la plantilla que utiliza django para sus proyectos:
   ```sh
    django-admin.exe startproject mysite .
   ```

   - Se modifica ciertas configuracion preestablecidas de mysite/settings.py , tales como fecha, ruta de archivos estaticos, base de datos, etc;
   ```sh
    ALLOWED_HOSTS = ['127.0.0.1', '.pythonanywhere.com']
    ...
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }
    ...
    LANGUAGE_CODE = 'es-es'
    TIME_ZONE = 'America/Lima'
    ...
    STATIC_ROOT = os.path.join(BASE_DIR, 'static')
    ...
    MESSAGE_STORAGE = 'django.contrib.messages.storage.session.SessionStorage'
   ```

   - En caso de presentarse error se recomienda añadir la siguiente linea al inicio del archivo settings.py:
   ```sh
    import os
   ```

   - Para crear una base de datos para nuestro blog, ejecutemos lo siguiente en la consola (necesitamos estar en el directorio principal que contiene el archivo manage.py):
   ```sh
    python manage.py migrate
   ```
   ```sh
     Operations to perform:
        Apply all migrations: admin, auth, contenttypes, sessions
     Running migrations:
        Applying contenttypes.0001_initial... OK
        Applying auth.0001_initial... OK
        Applying admin.0001_initial... OK
        Applying admin.0002_logentry_remove_auto_add... OK
        Applying admin.0003_logentry_add_action_flag_choices... OK
        Applying contenttypes.0002_remove_content_type_name... OK
        Applying auth.0002_alter_permission_name_max_length... OK
        Applying auth.0003_alter_user_email_max_length... OK
        Applying auth.0004_alter_user_username_opts... OK
        Applying auth.0005_alter_user_last_login_null... OK
        Applying auth.0006_require_contenttypes_0002... OK
        Applying auth.0007_alter_validators_add_error_messages... OK
        Applying auth.0008_alter_user_username_max_length... OK
        Applying auth.0009_alter_user_last_name_max_length... OK
        Applying auth.0010_alter_group_name_max_length... OK
        Applying auth.0011_update_proxy_permissions... OK
        Applying auth.0012_alter_user_first_name_max_length... OK
        Applying sessions.0001_initial... OK
   ```


   <h2>II. SOLUCION DE CUESTIONARIO</h2>

   - ¿Cuál es un estándar de codificación para Python? Ejemplo: Para PHP en el proyecto Pear https://pear.php.net/manual/en/standards.php
   - ¿Qué diferencias existen entre EasyInstall, pip, y PyPM?
   - En un proyecto Django que se debe ignorar para usar git. Vea: https://github.com/django/django/blob/main/.gitignore. ¿Qué otros tipos de archivos se deberían agregar a este archivo?
   - Utilice python manage.py shell para agregar objetos. ¿Qué archivos se modificaron al agregar más objetos?


   <h2>III. CONCLUSIONES</h2>


   <h1>RETROALIMENTACION GENERAL</h1>



   <h1>REFERENCIA Y BIBLIOGRAFIA</h1>

   -   https://www.w3schools.com/python/python_reference.asp
   -   https://docs.python.org/3/tutorial/
   -   https://developer.mozilla.org/es/docs/Learn/Server-side/Django/Models
   -   https://tutorial.djangogirls.org/es/django_models/
   -   https://pear.php.net/manual/en/standards.php
   -   https://docs.djangoproject.com/en/4.0/
   -   https://www.youtube.com/watch?v=M4NIs4BM1dk
   -   https://pypi.org/
   -   https://pip.pypa.io/en/latest/user_guide/
   -   https://packaging.python.org/en/latest/tutorials/installing-packages/

#

[Debian]: https://img.shields.io/badge/Debian-D70A53?style=for-the-badge&logo=debian&logoColor=white
[debian-site]: https://www.debian.org/index.es.html

[Git]: https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white
[git-site]: https://git-scm.com/

[GitHub]: https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white
[github-site]: https://github.com/

[Vim]: https://img.shields.io/badge/VIM-%2311AB00.svg?style=for-the-badge&logo=vim&logoColor=white
[vim-site]: https://www.vim.org/

[Java]: https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=java&logoColor=white
[java-site]: https://docs.oracle.com/javase/tutorial/


[![Debian][Debian]][debian-site]
[![Git][Git]][git-site]
[![GitHub][GitHub]][github-site]
[![Vim][Vim]][vim-site]
[![Java][Java]][java-site]


[![License][license]][license-file]
[![Downloads][downloads]][releases]
[![Last Commit][last-commit]][releases]
