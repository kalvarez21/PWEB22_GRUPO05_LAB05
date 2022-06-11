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

   - Se modifica ciertas configuraciones preestablecidas de mysite/settings.py , tales como fecha, ruta de archivos estaticos, base de datos, etc;
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

   <h3> CREACION DE MODELOS</h3>

   - Creamos una aplicacion (se creara una carpeta llamada blog en el directorio principal):
   ```sh
    python manage.py startapp blog
   ```

   - Luego añadimos la aplicacion al proyecto modificando en mysite/setting.py:
   ```sh
   INSTALLED_APPS = [
       'django.contrib.admin',
       'django.contrib.auth',
       'django.contrib.contenttypes',
       'django.contrib.sessions',
       'django.contrib.messages',
       'django.contrib.staticfiles',
       'blog.apps.BlogConfig', # linea agregada
    ]
   ```

   - Se crea el modelo POST, para ello en blog/models.py se borra y añade lo siguiente:
   ```sh
    from django.conf import settings
    from django.db import models
    from django.utils import timezone


    class Post(models.Model):
        author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
        title = models.CharField(max_length=200)
        text = models.TextField()
        created_date = models.DateTimeField(
                default=timezone.now)
        published_date = models.DateTimeField(
                blank=True, null=True)

        def publish(self):
            self.published_date = timezone.now()
            self.save()

        def __str__(self):
            return self.title
   ```

   - Una vez creado el modelo se tiene que crear el archivo de migracion ya que se modifico el antiguo modelo (ejecutar este codigo en el directorio principal):
   ```sh
     python manage.py makemigrations blog
   ```
   ```sh
     Migrations for 'blog':
       blog\migrations\0001_initial.py
         - Create model Post
   ```

   - Por ultimo se aplica a nuestro base de datos
   ```sh
     python manage.py migrate blog
   ```
   ```sh
   Operations to perform:
      Apply all migrations: blog
   Running migrations:
      Applying blog.0001_initial... OK
   ```

   <h3> ADMINISTRADOR DE DJANGO</h3>

   - Las funciones de agregar, editar y borrar posts se realizara por medio del administrador de DJango, para ello modificamos todo el contenido en blog/admin.py :
   ```sh
    from django.contrib import admin
    from .models import Post

    admin.site.register(Post)
   ```

   - Luego procedemos a crear un superusuario
   ```sh
     python manage.py createsuperuser
   ```
   ```sh
   Nombre de usuario (leave blank to use 'usuario'): kalvarez21
   Dirección de correo electrónico: kalvarez@unsa.edu.pe
   Password:
   Password (again):
   Superuser created successfully.
   ```

   - Una vez creado activamos el server y nos dirigimos a la direccion: http://127.0.0.1:8000/admin/
   ```sh
     python manage.py runserver
   ```
   - Dentro del link se podra visualizar:
      - Ventana de Login:
   <img src="https://i.ibb.co/yNJ0LSZ/image.png">
      - Ventana de Administracion de post y usuarios:
   <img src="https://i.ibb.co/C12cCxw/image.png">
      - Ventana de las funciones implementadas a post (agregar, editar):
   <img src="https://i.ibb.co/Sn1D0By/image.png">

   <h3> USANDO pythonanywhere</h3>

   - Primero tenemos que subir los archivos a un repositorio git tomando en cuenta el archivo .gitignore con el siguiente contenido:
   ```sh
    *.pyc
    *~
    __pycache__
    myvenv
    db.sqlite3
    /static
    .DS_Store
   ```

   - Luego tendremos que crear una cuenta en www.pythonanywhere.com para poder acceder a su bash(terminal). Para poder subir una aplicacion web se puede configurar de forma automatica escribiendo en el bash se pythonanywhere:
   ```sh
      pip3.6 install --user pythonanywhere
   ```
   ```sh
    ...
    Successfully built pythonanywhere
    Installing collected packages: contextlib2, typer, tabulate, schema, pythonanywhere
    Successfully installed contextlib2-21.6.0 pythonanywhere-0.10.2 schema-0.7.5 tabulate-0.8.9 typer-0.4.1
   ```

   - Ahora agregaremos la aplicacion que se estuvo trabajando en GitHub (bash pythonanywhere):
   ```sh
      pa_autoconfigure_django.py --python=3.6 https://github.com/kalvarez21/PWEB22_GRUPO05_LAB05.git
   ```

   - Despues de subir la aplicacion por completa se necesitara crear otra vez el superusuario ya que la base de datos no es la misma que la local (bash pythonanywhere).
   ```sh
      python manage.py createsuperuser
   ```

   - Ahora la pagina antes creada estara en internet, la URL tendra la forma http://(UsuarioDeTuCuenta).pythonanywhere.com/, ejm: http://kalvarez.pythonanywhere.com/ . Ademas si se desea activar a la ventana de logueo solo basta agregar al link la palabra admin.

   <h3> URLs en Django</h3>

   - Ahora empezaremos a redireccionar a la pagina que queremos que se muestre cuando se ingrese a http://127.0.0.1:8000/, para ello configuraremos en mysite/urls.py el contenido:
   ```sh
        from django.contrib import admin
        from django.urls import path, include

        urlpatterns = [
           path('admin/', admin.site.urls),
           path('', include('blog.urls')),
        ]
   ```

   - La linea 6 permitira que al ingresar al http://127.0.0.1:8000/ se rediriga a blog.urls y busque más instrucciones. Es por ello que tendremos que crear un archivo urls.py en la carpeta blog que contendra:
   ```sh
        from django.urls import path
        from . import views

        urlpatterns = [
            path('', views.post_list, name='post_list'),
        ]
   ```

   - NOTA: luego de seguir todo lo anterior ocurrira que al ingresar a http://127.0.0.1:8000/ nos salga error y si observamos en el cmd nos muestre una serie de mensajes, esto debido a que aun no hemos creado la pagina web sino que solo hemos redireccionado el link. Asi que solo para estar seguros de que todo se siguio correctamente por lo menos el ultimo de mensaje de error deberia ser:
   ```sh
        AttributeError: module 'blog.views' has no attribute 'post_list'
   ```

   <h3> Vistas en Django</h3>

   - Una View es un lugar donde ponemos la "lógica" de nuestra aplicación. Pedirá información del modelo que has creado antes y se la pasará a la plantilla. Para ello modificaremos en blog/views.py su contenido:
   ```sh
       from django.shortcuts import render

       # Create your views here.
       def post_list(request):
           return render(request, 'blog/post_list.html', {})
   ```

   - Esto nos mostrara:
   <img src="https://i.ibb.co/YRG9TFd/image.png">


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
