# Flask

Flask es un framework minimalista escrito en Python que permite crear aplicaciones web
rápidamente y con un mínimo de líneas de código, busca que su infraestructura inicial sea
lo más simple posible y pueda personalizarse fácilmente, puedes extender susfuncionalidades
con las llamadas Flask Extensions http://flask.pocoo.org/extensions/

## Environment Variables

    - FLASK_APP: es la variable para identificar el archivo donde se encuentra la aplicación.
    - FLASK_DEBUG: es la variable que se activa para realizar debug en el browser y para hot refresh.
    - FLASK_ENV=development : Para activar el development mode
    
| Nombre      |                      Descripcion                     |
|-------------|:----------------------------------------------------:|
| request     | Informacion sobre la peticion que realiza el browser |
| session     | Storage que permanece entre cada request             |
| current_app | La aplicacion actual                                 |
| g           | Storage temporal, se reinicia en cada request        |

## Request

```python
from flask import Flask, request

app = Flask(__name__)

@app.route("/")
def hello():
    user_ip = request.remote_addr
    return f"Hello World, your IP is {user_ip}"
```

## Response and Cookie

`Request-Response:` es uno de los métodos básicos que usan las computadoras para comunicarse
entre sí, en el que la primera computadora envía una solicitud de algunos datos y la segunda
responde a la solicitud.

Por lo general, hay una serie de intercambios de este tipo hasta que se envía el mensaje completo.

```python
from flask import Flask, request, make_response, redirect

app = Flask(__name__)

@app.route("/")
def index():
    user_ip = request.remote_addr
    response = make_response(redirect("/hello"))
    response.set_cookie("user_ip", user_ip)
    return response

@app.route("/hello")
def hello():
    user_ip = request.cookies.get("user_ip")
    return f"Hello World, your IP is {user_ip}"
```

## Templates con Jinja 2

Un templeate es un archivo de HTML que renderiza informacion (Estatica o Dinamica) por variables
que luego se nos muestra en el navegador.

Para renderizar un template/plantilla creada con Jinja2 simplemente hay que hacer uso del método
`render_template`.

A este método debemos pasarle el nombre de nuestra template y las variables necesarias para su 
renderizado como parámetros clave-valor.

Flask buscará las plantillas en el directorio templates de nuestro proyecto. En el sistema de
ficheros, este directorio se debe encontrar en el mismo nivel en el que hayamos definido nuestra
aplicación.

Se usan dobles llaves para pasar variables.

```
flask_project
|_ app.py
|_ /templates
    |_ hello.html
```

### html
```html
<h1>Hello World, your IP is {{ user_ip }}</h1>
```

### python

```python
# app.py

from flask import Flask, request, make_response, redirect, render_template

app = Flask(__name__)

@app.route("/")
def index():
    user_ip = request.remote_addr
    response = make_response(redirect("/hello"))
    response.set_cookie("user_ip", user_ip)
    return response

@app.route("/hello")
def hello():
    user_ip = request.cookies.get("user_ip")
    return render_template("hello.html", user_ip=user_ip)
```

## Estructuras de Control

### html

```html
{% if user_ip %}
    <h1>Hello World, your IP is {{ user_ip }}</h1>
{% else %}
    <a href="{{ url_for('index') }}">Ir a inicio</a>
{% endif %}
```

`Iteración:` es la repetición de un segmento de código dentro de un programa de computadora.
Puede usarse tanto como un término genérico (como sinónimo de repetición), así como para
describir una forma específica de repetición con un estado mutable.

Un ejemplo de iteración sería el siguiente:

```html
{% for key, segment in segment_details.items() %}
    <tr>
            <td>{{ key }}td>
            <td>{{ segment }}td>
    <tr>
{% endfor %}
```

En este ejemplo estamos iterando por cada segment_details.items() para mostrar los campos en
una tabla `{{ key }}` `{{ segment }}` de esta forma dependiendo de cuantos segment_details.items()
haya se repetirá el código.

### url_for

Genera una URL del endpoint de acuerdo al metodo pasado en la funcion.

## Herencia de Templates

Se usa el keyword **extends** para la herencia, y **block** para organizar nuestra informacion en el archivo heredado.

### html parent

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8"/>
        <title>{% block title %}Flask | {% endblock %}</title>
    </head>
    <body>
        {% block content %}
        {% endblock %}
    </body>
</html>
```

### html

```html
{% extends 'archivo_base.html' %}

{% block title %}
    {{ super() }}
    Bienvenido
{% endblock %}

{% block content %}

    {% if user_ip %}
        <h1>Hello World, your IP is {{ user_ip }}</h1>
    {% else %}
        <a href="{{ url_for('index') }}">Ir a inicio</a>
    {% endif %}

{% endblock %}
```

Macro: son un conjunto de comandos que se invocan con una palabra clave, opcionalmente seguidas de parámetros que se utilizan como código literal. Los Macros son manejados por el compilador y no por el ejecutable compilado.

Los macros facilitan la actualización y mantenimiento de las aplicaciones debido a que su re-utilización minimiza la cantidad de código escrito necesario para escribir un programa.

### macros.html

```html
{% macro render_something(variable) %}
    <h1>{{ variable }}</h1>
{% endmacro %}
```

```html
{% import "macros.html" as macros %}

{{ macros.render_something("Valor") }}
```

## Include y Links

### navbar.html
```html
<nav>
    <ul>
        <li><a href="{{ url_for('index') }}">Ir a inicio</a></li>
        <li><a href="http://google.com" target="_blank">Ir a Google</a></li>
    </ul>
</nav>
```

### html parent

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8"/>
        <title>{% block title %}Flask | {% endblock %}</title>
    </head>
    <body>
        <header>
            {% include "navbar.html" %}
        </header>
        {% block content %}
        {% endblock %}
    </body>
</html>
```

## Archivos estaticos

```
flask_project
|_ app.py
|_ /static
    |_ /css
        |_ main.css
    |_ /images
        |_ logo.png
|_ /templates
    |_ index.html
    |_ navbar.html
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8"/>
        <title>{% block title %}Flask | {% endblock %}</title>
        <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}"/>
    </head>
    <body>
        <header>
            {% include "navbar.html" %}
        </header>
        {% block content %}
        {% endblock %}
    </body>
</html>
```


```html
<nav>
    <ul>
        <img src="{{ url_for('static', filename='images/logo.png') }}" alt="Logo"/>
        <li><a href="{{ url_for('index') }}">Ir a inicio</a></li>
        <li><a href="http://google.com" target="_blank">Ir a Google</a></li>
    </ul>
</nav>
```

## Manejo de Errores

100: no son errores sino mensajes informativos. Como usuario nunca los verás, sino que entre bambalinas indica que la petición se ha recibido y se continúa el proceso.

200: estos códigos también indican que todo ha ido correctamente. La petición se ha recibido, se ha procesado y se ha devuelto satisfactoriamente. Por tanto, nunca los verás en tu navegador, pues significan que todo ha ido bien.

300: están relacionados con redirecciones. Los servidores usan estos códigos para indicar al navegador que la página o recurso que han pedido se ha movido de sitio. Como usuario, no verás estos códigos, aunque gracias a ellos una página te podría redirigir automáticamente a otra.

400: corresponden a errores del cliente y con frecuencia sí los verás. Es el caso del conocido error 404, que aparece cuando la página que has intentado buscar no existe. Es, por tanto, un error del cliente (la dirección web estaba mal).

500: mientras que los códigos de estado 400 implican errores por parte del cliente (es decir, de parte tuya, tu navegador o tu conexión), los errores 500 son errores desde la parte del servidor. Es posible que el servidor tenga algún problema temporal y no hay mucho que puedas hacer salvo probar de nuevo más tarde.

```html
{% extends 'archivo_base.html' %}

{% block title %}
    {{ super() }}
    Error 404
{% endblock %}

{% block content %}
    <p>{{ error }}</p>
{% endblock %}
```

```python
@app.errorhandler(404)
def not_found(error):
    return render_template(".html", error=error)
```

## Extensiones de Flask

### Flask Bootstrap

Framework: es un conjunto estandarizado de conceptos, prácticas y criterios para enfocar un tipo de problemática particular que sirve como referencia, para enfrentar y resolver nuevos problemas de índole similar.

`pip install Flask-Bootstrap4`

Bootstrap ya posee un base.html, se implementaria asi

```html
{% extends 'bootstrap/base.html' %}

{% block head %}
    {{ super() }}
    
    <title>{% block title %}Flask | {% endblock %}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}"/>
{% endblock %}

{% block body %}
    {% block navbar %}
        {% include 'navbar.html' %}
    {% endblock %}
    {% block content %}{% endblock %}
{% endblock %}
```

```python
from flask_bootstrap import Bootstrap

app = Flask(__name__)
bootstrap = Bootstrap(app)
```

| Block Name   |  Outer Block | Purpose                                             |
|--------------|:------------:|-----------------------------------------------------|
| doc          |              | Outermost block                                     |
| html         | doc          | contains the complete content of the `<html>` tag   |
| html_attribs | doc          | Attributes for the HTML tag                         |
| head         | doc          | Contains the complete content of the `<head>` tag   |
| body         | doc          | Contains the complete content of the `<body>` tag   |
| body_attribs | body         | Attributes for the Body tag                         |
| title        | head         | Contains the complete content of the `<title>` tag  |
| styles       | head         | Contains all CSS style `<link>` tags inside head    |
| metas        | head         | Contains all `<meta>` tags inside head              |
| navbar       | body         | An empty block directly above content               |
| content      | body         | Convenience block inside the body. Put stuff here   |
| scripts      | body         | Contains all `<script>` tags at the end of the body |

### Flask WTF

`pip install Flask-WTF`

```html
{% import 'bootstrap/wtf.html' as wtf %}

<div>
    <form action="{{ url_for('hello') }}" method="POST">
        {{ login_form.username }}
        {{ login_form.username.label }}
        {{ login_form.password }}
        {{ login_form.submit }}
        
        
        {{ wtf.quick_form(login_form) }}
    </form>
</div>
```

```python
from flask_wtf import FlaskForm
from wtforms.validators import DataRequired
from wtforms.fields import StringField, PasswordField, SubmitField

app = Flask(__name__)

class LoginForm(FlaskForm):
    username = StringField('Nombre de usuario', validators=[DataRequired()])
    password = PasswordField('Password', validators=[DataRequired()])
    submit = SubmitField("Enviar")
    
@app.route("/")
def hello():
    return render_template("index.html", login_form=LoginForm())
```

## Session

Es un intercambio de información interactiva semipermanente, también conocido como diálogo, una conversación o un encuentro, entre dos o más dispositivos de comunicación, o entre un ordenador y usuario.

```python
from flask import Flask, request, make_response, redirect, session, render_template

app = Flask(__name__)

app.config["SECRET_KEY"] = "CLAVE SECRETA"

@app.route("/")
def index():
    user_ip = request.remote_addr
    response = make_response(redirect("/hello"))
    session['user_ip'] = user_ip
    
    return response

@app.route("/hello")
def hello():
    user_ip = session.get("user_ip")
    return render_template("hello.html", user_ip=user_ip)
```

Flask acepta peticiones GET por defecto y por ende no debemos declararla en nuestras rutas.

Pero cuando necesitamos hacer una petición POST al enviar un formulario debemos declararla de la siguiente manera, como en este ejemplo:

`@app.route('/platzi-post', methods=['GET', 'POST'])`

Debemos declararle además de la petición que queremos, GET, ya que le estamos pasando el parámetro methods para que acepte solo y únicamente las peticiones que estamos declarando.

De esta forma, al actualizar el navegador ya podremos hacer la petición POST a nuestra ruta deseada y obtener la respuesta requerida.

```python
from flask_wtf import FlaskForm
from wtforms.validators import DataRequired
from wtforms.fields import StringField, PasswordField, SubmitField

app = Flask(__name__)

class LoginForm(FlaskForm):
    username = StringField('Nombre de usuario', validators=[DataRequired()])
    password = PasswordField('Password', validators=[DataRequired()])
    submit = SubmitField("Enviar")
    
@app.route("/", methods=["GET", "POST"])
def hello():
    login_form = LoginForm()
    
    if login_form.validate_on_submit():
        username = login_form.username.data
        password = login_form.password.data
    
    return render_template("index.html", login_form=login_form)
```

### Filtros

```html
{{ username | capitalize }}
```

## Desplegar Flashes (mensajes emergentes)

```html
{% block body %}
    {% block navbar %}
        {% include 'navbar.html' %}
    {% endblock %}
    
    {% for message in get_flashed_messages() %}
        <div>{{ message }}</div>
    {% endfor %}

    {% block content %}{% endblock %}
{% endblock %}
```

```python
from flask import flash

# Esto se debe poner antes de retornar el template
flash("Mensaje desplegable")
```

## Importar Scripts

```html
{% block scripts %}
    {{ super() }}
{% endblock %}
```

## Flask testing

La etapa de pruebas se denomina testing y se trata de una investigación exhaustiva, no solo técnica sino también empírica, que busca reunir información objetiva sobre la calidad de un proyecto de software, por ejemplo, una aplicación móvil o un sitio web.

El objetivo del testing no solo es encontrar fallas sino también aumentar la confianza en la calidad del producto, facilitar información para la toma de decisiones y detectar oportunidades de mejora.

`pip install flask-testing`

Se buscan los test en la ruta *tests*

`flask test`

```python
@app.cli.command()
def test():
    tests = unittest.TestLoader().discover("tests")
    unittest.TextTestRunner().run(tests)
```

```python
from flask_testing import TestCase
from flask import current_app

from main import app


class MainTest(TestCase):
    def create_app(self):
        app.config["TESTING"] = True
        app.config["WTF_CSRF_ENABLED"] = False
        
    def test_app_exists(self):
        self.assertIsNotNone(current_app)
        
    def test_app_in_test_mode(self):
        self.assertTrue(current_app.config["TESTING"])
        
    def test_index_redirect(self):
        response = self.client.get(url_for("index"))
        self.assertRedirects(response, url_for('hello'))
        
    def test_hello_get(self):
        response = self.client.get(url_for("hello"))
        self.assert200(response)
        
    def test_hello_post(self):
        fake_form = {
            'username': 'vijoin',
            'password': '123456'
        }
        self.client.post(url_for('index'), data=fake_form)
        
        self.assertRedirects(response, url_for('index'))
        self.assert_message_flashed('User registered successfully')
```

## Blueprint

Pequeña aplicacion de Flask que tiene rutas, vistas y templates