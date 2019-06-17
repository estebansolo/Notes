# Deployments

## Tabla de Contenido

- [Introduction](#introduction)
    - [CDN](#cdn)
    - [API](#api)
    - [Aplicaciones Monoliticas](#aplicaciones-monoliticas)
    - [Microservicios](#microservicios)
- [Opciones para hacer deploy](#opciones-para-hacer-deploy)
    - [Amazon Web Services](#amazon-web-services)
    - [Microsoft Azure](#microsoft-azure)
    - [Google Cloud Plaform](#google-cloud-plaform)
    - [Digital Ocean](#digital-ocean)
    - [Zeit](#zeit)
    - [Heroku](#heroku)
    - [GitHub Pages](#gitHub-pages)
    - [Surge](#surge)

## Introduction

### CDN

Content Delivery Network. Muchos servidores distribuidos por todo el mundo proveer de estos archivos comunes y que no están generados dinámicamente a nuestros usuarios y que puedan acceder rápidamente a ellos.

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### API

Aplication Programming Interface. Representa la capacidad de comunicación entre componentes de software.

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Aplicaciones Monoliticas

#### Ventajas

  - Buena para aplicaciones pequeñas.
  - Fácil de desarrollar.
  - Fácil de hacer deploy.
  - Fácil para trabajar individual o en equipos pequeños.

#### Desventajas

  - Difícil de mantener a largo plazo.
  - Costosa para escalar.
  - En caso de un error se puede caer toda la aplicación.
  - Más difícil testear.
  - Más difícil de depurar.

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Microservicios

¿Qué es un microservicio?
El código dividido en varias aplicaciones.

#### Ventajas

  - Fácil de hacer deploy.
  - Fácil de escalar.
  - Fácil de testear.
  - Fácil de depurar.
  - En caso de error solo se cae un servicio.
  - Se pueden utilizar diferentes tecnologías.

#### Desventajas

  - Difícil de orquestar.
  - Puede ser lenta la comunicación entre servicios.
  - Difícil saber cómo dividir nuestra aplicación.
  - Es más costoso de mantener.

Importante:

Orquestación y Coreografía de Servicios = Ambos conceptos se basan en cómo hacer para comunicar nuestros servicios y que todo funcione como si fuera una sola aplicación.

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Opciones para hacer deploy

### Amazon Web Services

Con control de infraestructura, Es el más grande de todas las opciones para hacer deploy.

Ver mas: [Amazon Web Services]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Microsoft Azure

Con control de infraestructura, Perfecto para aplicaciones en C# y .Net

Ver mas: [Microsoft Azure]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Google Cloud Plaform

Con control de infraestructura, Una ventaja es que tiene varias API propias de Google que se pueden integrar en la aplicación.

Ver mas: [Google Cloud Plaform]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Digital Ocean

Con control de infraestructura, Permite tener un servidor privado y empezar a encontrar todo lo que se quiere ahí.

Ver mas: [Digital Ocean]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Zeit

Sin control de infraestructura,

Deploy de cualquier tipo, incluso contenedores de Docker. Solo se pueden usar con servidores Web.

Ventajas al momento de hacer deploy.

#### Tipos de deploy:
  - Aplicaciones Node.js
  - Sitios Estaticos
  - Contenedores Docker

#### Caracteristicas:
  - Es facil.
  - Escala automaticamente.
  - Deploy inmutables, cada deploy retorna una URL a la cual se puede acceder.
  - Deploy sin caida.
  - Deploy Ilimitados
  - HTTP2 Automaticamente
  - Certificado SSL Gratis
  - Logs por cada Deploy
  - DNS (zeit.world)
  - Comprar Dominios por CLI

Ver mas: [Zeit]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Heroku

Sin control de infraestructura, Permite hacer deploy sin tener que pensar en cómo va a funcionar al app por debajo ni la infraestructura de esta.

Ver mas: [Heroku]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### GitHub Pages

Sitios estaticos, Permite hacer el deploy de archivos estáticos. Es completamente gratis pero el código es open source.

El proyecto debe estar publico, se usa principalmente para documentar librerias

  - settings
  - seccion github pages
  - debe ser aster branch
  - (save)

Ver mas: [GitHub Pages]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Surge

Sitios estaticos, Permite hacer deploys estáticos muy fácilmente por medio de un CLI.

```
npm i -g surge
```

Ir a la carpeta 

```
surge
```
usar datos de login

Ver mas: [Surge.sh]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>




elephantsql

# INstalando now.sh

```
npm install -g now
```

Desplegar proyecto, entrar a la carpeta del prroyecto


1. Ir a la capeta del proyecto
2. Escribir el comando now.


```
now
```

Podemos cambiar el nombre de la url generada, se puede hacer de la siguiente manera:

o en el archivo now.json

"alias" : "alias.now.sh"

```
now alias {URL_GENERADA} {NOMBRE}.now.sh
```


    now Ejecuta el deploy (de todos los archivos de la carpeta donde se encuentra posicionado).
    now [directorio del proyecto] Ejecuta el deploy de todos los archivos de la carpeta indicada.
    now [user]/[repositorio] Ejecuta un deploy partiendo de un repositorio en GitHub.
    now -e NODE_ENV=production -e MONGODB_PASSWORD=@password Ejecuta un deploy con variables de entorno.
    now alias [URL generada por Now.sh] [URL personalizada].now.sh Permite crear un alias de la dirección URL.

https://joaquinaraujo.github.io/deploy-now/

Si se presenta algun error, en la raiz del proyecto crear un archivo now.json con el siguiente contenido

```json
{
  "version": 1
}
```

eliminar instancia creada

```
now rm [url]
```

## Deploy de applicacion Node

Para hacer deploy a una aplicación en node.js, hay que crear un archivo now.json.
En ese eschivo, escribir lo siguiente:

{
  "name": "{NOMBRE DE LA APP}",
  "type": "npm"
}


## Deploy de docker

Para hacer deploy a una aplicación Docker, hay que crear un archivo now.json.
En ese eschivo, escribir lo siguiente:

{
  "name": "{NOMBRE DE LA APP}",
  "type": "docker"
}


* pubsub = Nos sirve para tener una forma de comunicarnos cuando hacemos la parte de las suscripciones en real time.
* resolvers = Nos sirven para saber qué hacer en cada query o cada cambio que el navegador envía al API.
* squema = Le escribimos todo el esquema de datos que tiene nuestra aplicación, los datos que existen.
* server = Donde inicializamos el servidor, sincronizamos el modelo con la base de datos, creamos el servidor express y creamos todo lo que necesitamos para correr en producción.

## Secret y Variables de entorno

"env" : {
    "KEY" : "VALUE"
}

```
now secrets
```

```
now secrets add (snake_case) {VAR_NAME} "[VAR_VALUE]" 
```

"env" : {
    "KEY" : "@secret"
}

## Ver codigo fuente

despues de la url agregar _src // public
_log // privado


```
now alias
```

ultimo deploy al alias definido en el now.json

## Dominio

zeit.world

DNS gratuito global

al tener el dominio

  - custom dns
  - poner los dns definidos

comprar dominios

```
now domain buy [URL].com 
```


mostrar ultimos deploys
```
now ls
```

now alias [URL GENERADA] [CUSTOM DOMAIN]


https://platzi.com/comentario/349139/
https://github.com/platzi/now-course
https://zeit.co/docs/
https://platzi.com/comentario/331097/

## Componer microservicios

rules.json

 {
    "rules": [
        {
            "pathname": "/graphql",
            "dest": "[aplicacion].now.sh"
        },
        {
            "pathname": "/[ruta]",
            "dest": "[aplicacion].now.sh"
        },
        {
            "dest": "[aplicacion].now.sh"
        }
    ]
}


La forma de establecer esta configuración en Now.sh es por medio de el comando:

now alias [aplicacion].now.sh -r rules.json Permite establecer las configuraciones de rules.json en un deploy de Now.sh.

## Deploy desde github

```
now user/proyecto
```



[Amazon Web Services]: <https://aws.amazon.com/>
[Microsoft Azure]: <https://azure.microsoft.com/en-us/>
[Google Cloud Plaform]: <https://cloud.google.com/>
[Digital Ocean]: <https://www.digitalocean.com/>
[Zeit]: <https://zeit.co/>
[Heroku]: <https://www.heroku.com/>
[GitHub Pages]: <https://pages.github.com/>
[Gitlab Pages]: <https://about.gitlab.com/product/pages/>
[Surge]: <https://surge.sh/>