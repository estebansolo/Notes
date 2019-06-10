# Sass Course

## Contents
- [Test Sass Code](#test-sass-code)
- [Sass file extensions](#sass-file-extensions)
- [Import Partials](#import-partials)
- [Variables](#variables)



  - [Escapar una variable](#escapar-una-variable)
- [Anidaciones](#anidaciones)
- [Mixins](#mixins)
  - [Content](#content)
- [Extend](#extend)
- [Funciones](#funciones)
  - [Crear funciones](#crear-funciones)
- [Array](#array)
- [Controles de Flujo](#controles-de-flujo)
  - [each](#each)
  - [for](#for)
  - [if](#if)
- [Enlaces de Interés](#enlaces-de-interés)

## Test Sass Code

[Sass Meister](https://www.sassmeister.com/) is a tools that allow us to prove our sass code and see how it works

<div align="right">
  <small><a href="#contents">🡡 volver al inicio</a></small>
</div>

## Sass file extensions

Sass provide two extensions

```sass
.sass or .scss
```
<a href="https://sass-lang.com/documentation/syntax" target="_blank">Syntax Documentation</a>

<div align="right">
  <small><a href="#contents">🡡 volver al inicio</a></small>
</div>

## Import Partials

Una ventaja que trae Sass es el poder organizar mejor nuestros archivos. Esto lo podemos lograr separando nuestros estílos en múltiples archivos. De tal modo, ya no tenemos que revisar un archivo muy amplio, sino que podemos separar nuestros estilos en varios módulos haciendo el trabajo mucho más fácil.

Todos los import van en un solo archivo con el fin de compilar este unico archivo, para organizar e importar archivos usamos `@import`.

```sass
@import "headers"
```

La forma de nombrar los parciales que seran importados es con un `_` al inicio, sin embargo el compilador reconoce los archivos sin tener la extension ni el `_`.

```
eg: _headers.sass
```

<div align="right">
  <small><a href="#contents">🡡 volver al inicio</a></small>
</div>

## Variables

Las variables son una forma de almacenar la información que se desea reutilizar. 

Se puede almacenar diferentes valores: colores, fuentes, tamaños y cualquier valor que se desee reutilizar. Sass usa el símbolo `$` para hacer que algo sea una variable. 

Ejemplo:

```sass
$font-stack: Helvetica, sans-serif
$primary-color: #333

body {
  font: 100% $font-stack
  color: $primary-color
}
```

`BEM` — Block Element Modifier o Modificador de Bloques de Elementos

Como su nombre indica, BEM distingue claramente 3 conceptos: el Bloque, el Elemento y el Modificador.

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>





### Escapar una variable

Para escapar una variable se usa el comodín `#` ademas de las llaves. 

Esto es necesario en casos como, por ejemplo, cuando la variable está rodeada por comillas y de no ponerse el escape la variable pasaría como una cadena de caracteres..

```sass
$size: 10;

div {
  content: "#{$size}"
}
```

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>

## Anidaciones

```sass
.btn {  
  font-size: 15pt;
  &__icon {
    font-size: .6em;
  }
  &.btn--info {
    background-color: $color-info;
  }
}
```

El comodín `&` se usa para hacer referencia al padre.

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>



~~~
.btn{
	display: inline-block;
	color: #fff;
	background-color: #333;
	border-radius: 5px;

	.btn__icon{
		font-size: 24px;
	}

	.btn--info{
		background-color: skyblue;
	}
}
~~~



## Mixins

Los mixins nos ayudan a reciclar declaraciones para evitar mucho trabajo. Para esto vamos a usar @`mixin`.

Cuando se define un mixin, los argumentos se definen como una serie de variables separadas por comas, y todo ello encerrado entre paréntesis.

```sass
@mixin max-width($max-width: 800px) {
  max-width: $max-width
  margin-left: auto
  margin-right: auto
}
```

En este caso le estamos definiendo un valor por defecto. Si deseamos cambiar ese valor, cuando lo llamemos se lo podemos cambiar de esta forma:

```sass
@mixin max-width(1200px)
```

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>



```sass
@mixin h1
    h1
        margin: 0
        padding: 0


@mixin wrap-width($width: $wrapper-width)
    width: $width
    margin: 0 auto

@include h1
@influde wrap-width(500px)
```


Los mixins permiten definir estilos reutilizables en toda la hoja de estilos.
Se definen con la directiva **@mixin** seguida del nombre del mixin

Los mixins se incluyen en las hojas de estilos mediante la directiva **@include** seguida del nombre del mixin y opcionalmente por una lista de argumentos.

```sass
@mixin max-width($max-width: 800px) {
	max-width: $max-width;
	margin-left: auto;
	margin-right: auto;
}

.container{
	@include max-width(1200px);
}

section{
	@include max-width(800px);
	background-color: #333;
	padding: 15px;
}
```

#### propios

Los **mixins **nos permite recibir parámetros, esta funcionalidad nos ayuda bastante, ya que con un solo mixins podemos obtener distintas salidas con solo cambiar el valor del parámetro.
Ejemplo: Nos ayuda bastante al momento de realizar mediaqueries

@mixin encabezados($size)
  h1
    font-size: $size

  h2
    font-size: $size - 0.2

  h3
    font-size: $size - 0.5

@include encabezados(1.5em)
@media(min-width: 800px)
  @include encabezados(2em)


BEM block element modifier
organizar el css

bloque:
.btn
  elemento
    .btn__icon

  modificador
    .btn--warning
    mismas propiesdades excepto cambios visuales





### Content

Una de las características que tienen los mixins es la directiva content. Esta nos permite incluir un bloque de contenido dentro de un mixin.

```sass
@mixin response-to($width) {
  @media only screen and (min-width: $width) {
    @content;
  }
}
```

Se usa de esta forma:

```sass
section {
  background: blue;
  @include response-to(800px) {
    background-color: red;
  };
}
```

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>



Nos permite incluir un bloque de contenido dentro de un mixin.

**Entrada:**

~~~
@mixin respond-to($width){
  @media only screen and (min-width: $width){
    @content;
  }
}

section{
  background-color: skyblue;
  @include respond-to(800px){
    background-color: teal;
  }
}
~~~

**Salida:**

~~~
section {
  background-color: skyblue;
}

@media only screen and (min-width: 800px) {
  section {
    background-color: teal;
  }
}
~~~


@content
incluir un bloque dentro de un mixing



## Extend

Permiten que una declaración herede estilos declarados por otra regla o placeholder. Los extend se declaran con el símbolo de porcentaje `%`.

```sass
%btn {
  color: red;
  width: 50px;
}

.btn-info {
  @extend %btn;
  background: blue;
}
```

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>


Nos permite crear un fragmento de estilos que luego podamos reutilizar fácilmente en cualquier componente.

**Entrada:**

~~~
%max-width{
  max-width: 80%;
  margin: 0 auto;
}

.section{
  @extend %max-width;
}

.container{
  @extend %max-width;
}
~~~

**Salida:**

~~~
.section, .container {
  max-width: 80%;
  margin: 0 auto;
}
~~~


@extends
Incluir los estilos de un elemento en otro

placeholder %btn
no aparece en el css hasta influirlo

%max-width
  max-width: 80%
  margin: 0 auto

.section
  @extend %max-width



## Funciones

Sass tiene muchas funciones que podemos usar cuando estamos modificando CSS. Muchas de estas funciones son muy útiles como por ejemplo aclarar un color u oscurecerlo. 

```sass
darken(#ffffff, 25%)
lighten(#ffffff, 25%)
invert(#ffffff)
```

La lista completa de funciones se pueden ver aquí:
https://sass-lang.com/documentation/file.SASS_REFERENCE.html#functions

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>



**Entrada:**

~~~
@function suma($num-uno, $num-dos){
  @return $num-uno + $num-dos;
}

.div{
  padding: suma(12, 6);
}


$fs: (
  big: 24px,
  normal: 16px,
  small: 14px,
  x-small: 12px
);

p{
  font-size: map-get($fs, normal);
}

small{
  color: #333;
  font-size: map-get($fs, small);
}
~~~

**Salida:**

~~~
.div {
  padding: 18;
}

p {
  font-size: 16px;
}

small {
  color: #333;
  font-size: 14px;
}
~~~

#### propio


Functiones
Sass tiene muchas funciones que podemos usar cuando estamos modificando CSS. Muchas de estas funciones son muy útiles como por ejemplo aclarar un color u oscurecerlo.

darken(#ffffff, 25%)
lighten(#ffffff, 25%)
invert(#ffffff)

La lista completa de funciones se pueden ver aquí:
https://sass-lang.com/documentation/file.SASS_REFERENCE.html#functions



https://github.com/MineiToshio/CursosPlatzi/tree/master/Curso%20de%20Sass
https://sass-lang.com/documentation/functions


### Crear funciones

```sass
@function suma($numero-uno, $numero-dos) {
  @return $numero-uno + $numero-dos;
}

.div {
  padding: suma(10px, 5px);
}
```

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>


@function suma($num-uno, $num-dos)
  @return $num-uno + $num-dos


.h1
  padding: suma(20px, 10px)


.h1{
  padding: 30px;
}



## Array

```sass
$fs: (
  big: 24px,
  normal: 16px,
  small: 14px,
  x-small: 12px
);

p {
  font-size: map-get($fs, normal);
}

small {
  font.size: map-get($fs, x-small);
}
```

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>


Mapas (Dict)
$fs : (
  big: 24px,
  normal: 16px,
  small: 14px,
  xsmall: 12px
)

p
  font-size: map-get($fs, normal)

small
  font-size: map-get($fs, small)







## Controles de Flujo

### each

```sass
$font-weights: normal bold italic;

@each $font in ($font-weights) {
  .#{$font} {font.weight: $font;}
}
```

y esto da como resultado:

```css
.normal {
  font-weight: normal;
}

.bold {
  font-weight: bold;
}

.italic {
  font-weight: italic;
}
```

<div align="right">
  <small><a href="#tabla-de-contenido">🡡 volver al inicio</a></small>
</div>


**Entrada:**

~~~
$font-weights: normal bold italic;

@each $font in ($font-weights){
  .#{$font} {
    font-weight: $font;
  }
}
~~~

**Salida:**

~~~
.normal {
  font-weight: normal;
}

.bold {
  font-weight: bold;
}

.italic {
  font-weight: italic;
}
~~~

#### propio

each (cliclo)

@each $font in (normal, bold, italic)
  .text-#{$font}
    font-weight: $font

$fw : normal, bold, italic
@each $font in ($fw)
  .text-#{$font}
    font-weight: $font




### for

```sass
@for $i from 1 to 5 {
  .class-#{$i} {
    &:before {
      content: "#{$i}"
    }
  }
}
```

Resultado:

```css
.class-1:before {
  content: "1";
}

.class-2:before {
  content: "2";
}

...

.class-5:before {
  content: "5";
}
```

<div align="right">
  <small><a href="#contents">🡡 volver al inicio</a></small>
</div>


**Entrada:**

~~~
@for $i from 1 to 5{
  .class-#{$i}{
    &:before{
      content: "#{$i}";
    }
  }
}
~~~

**Salida:**

~~~
.class-1:before {
  content: "1";
}

.class-2:before {
  content: "2";
}

.class-3:before {
  content: "3";
}

.class-4:before {
  content: "4";
}
~~~


#### propio

  for (ciclo)

from
1 - 5 itera 4
@for $var from <inicio> to <fin>{ ... }

  @for $i from 1 to 5
    .class-#{$i}
      &::before
        content: "#{$i}"

through
@for $var through <inicio> to <fin>{ ... }
1 - 5 itera 5






### if

```sass
$background-color: black;

@if $background-color == black {
  p {
    text-color: white;
  }
}
@else {
  p {
    text-color: black;
  }
}
```

<div align="right">
  <small><a href="#contents">🡡 volver al inicio</a></small>
</div>


**Entrada:**

~~~
$background: black;

@if $background == black{
  p{
    color: white;
  }
}
@else{
  p{
    color: black;
  }
}
~~~

**Salida:**

~~~
p {
  color: white;
}
~~~



#### propio

if

p
  text-color: blue

$background-color : black
@if $background-color == black 
  p
    text-color: $background-color
@else
  p
    text-color: white





## Enlaces de Interés
* [Curso de Sass](https://platzi.com/clases/sass/)

<div align="right">
  <small><a href="#contents">🡡 volver al inicio</a></small>
</div>




### Enlaces de interes ###

[SASS - Documentación Oficial](https://sass-lang.com/) <br>
[SASS Functions](http://sass-lang.com/documentation/Sass/Script/Functions.html) <br>
[BEM](http://getbem.com/introduction/) <br>
[SASS Meister](https://www.sassmeister.com/) <br>
[Funciones nativas de SASS](https://styde.net/lista-completa-de-funciones-nativas-de-sass/) <br>







En el reto anterior el profesor propuso crear una función que nos permita manejar los z-index de nuestro proyecto. Para esto, lo primero que debemos hacer es definir cuales son las respectivas propiedades y valores que vamos a manejar. En este caso decidí que los elementos que suelen tener la propiedad de z-index son:

    Los dropdown que contenga mi proyecto.
    Los elementos sticky.
    Los modales
    El overlay de cada modal
    Los tooltip

Una vez definido esto, vamos a asignarle un valor. Es importante que no sean valores seguidos, ya que puede que necesitemos agregar la propiedad de z-index a elementos individuales en el camino y no queremos que se pisen. Para esto, dejaremos un margen de 20 entre cada uno.

$fs: ( 
	zindex-dropdown: 100, 
	zindex-sticky: 120, 
	zindex-modal: 140, 
	zindex-overlay:160,
	zindex-tooltip:180
);