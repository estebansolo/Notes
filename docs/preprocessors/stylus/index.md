# Stylus Course

## Introduction

In Stylus it is not necessary to use brackets or semicolons.

```
.styl
```

[Try Stylus]

## Import Partials

One advantage of Stylus is the ability to organize our files. We can do this by separating our styles into different files. This way, we no longer have to handle large files, but we can separate them making the job much easier.

Imports can be made in any file, however you must make a main file in order to compile this one file. To import files we use `@import`.

```
@import "_headers.styl"
```

The way to name the partials that will be imported is with a `_` at the beginning, however the compiler recognizes the files without having the extension or the `_`.

```
file eg: _headers.styl
```

We can import all the files inside a folder

```
@import 'libs/*'
```


## Variables

Variables are a way of storing the information you want to reuse, you can store different values: colors, fonts, sizes and any value you want to reuse. To create a variable we must assign it a value with the equal sign `=`

```
font-stack = Helvetica, sans-serif
primary-color = #333

body
  font: 100% font-stack
  color: primary-color
```

Output:

```
body {
	font: 100% Helvetica, sans-serif;
	color: #333;
}
```


## Nesting

```
.container, .redtext
  color: red
  > .first-child
    margin-bottom: 20px
  &:before
    content: "Hi"
```

Output:

```
.container,
.redtext {
	color: #f00;
}

.container > .first-child,
.redtext > .first-child {
	margin-bottom: 20px;
}

.container:before,
.redtext:before {
	content: "Hi";
}
```

The wildcard `&` is used to refer to the parent.

## Mixins

The mixins allow to define reusable styles in all the stylesheet, the mixins allow us to receive parameters, this functionality helps us a lot, since with only one mixins we can obtain different outputs with only changing the value of the parameter. The names should have names different to the styles, we can use the prefix `mixin`

```
mixin-max-width(m-width = 800px)
  max-width: m-width
  margin-left: auto
  margin-right: auto

.container
  mixin-max-width()

.section
  margin-bottom: 24px
  mixin-max-width(80vw)
```

Output:

```
.container {
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}
.section {
  margin-bottom: 24px;
  max-width: 80vw;
  margin-left: auto;
  margin-right: auto;
}
```


### Create a function

```
mixin-padding-small(a, b)
  a + b

.div
  padding: mixin-padding-small(10px, 8)
```

Output:

```
.div {
  padding: 18px;
```


## Operator

Stylus has Operators that we can use, these can be + , - , / , *

```
padding = 20px
small-padding = padding / 2
```


## For

```
.div
  for x in 0 1 2 3
    content: x

.div
  for x in (0..3)
    content: x

gridsize = (1..6)
for size in gridsize
  .container-item-{size}
    width: (100 / size) * 1%
```

Output:

```
.div {
  content: 0;
  content: 1;
  content: 2;
  content: 3;
}
.div {
  content: 0;
  content: 1;
  content: 2;
  content: 3;
}
.container-item-1 {
  width: 100%;
}
.container-item-2 {
  width: 50%;
}
.container-item-3 {
  width: 33.333333333333336%;
}
.container-item-4 {
  width: 25%;
}
.container-item-5 {
  width: 20%;
}
.container-item-6 {
  width: 16.666666666666668%;
}
```

or

```
flag-url = "https://image.flaticon.com/sprites/new_packs/551843-square-country-simple-flags.png"

flags = { uk: -36px, usa: -236px, japan: -436px }

.container
	border: 1px solid red;

.flag
  width: 130px
  height: 128px
  background-position-y: -30px
  background-image: url(flag-url)

for flag in flags
  .flag.flag-{flag}
    background-position-x: flags[flag]
```

Output:

```
.container {
  border: 1px solid #f00;
}
.flag {
  width: 130px;
}
height: 128px {
  background-position-y: -30px;
  background-image: url("https://image.flaticon.com/sprites/new_packs/551843-square-country-simple-flags.png");
}
.flag.flag-uk {
  background-position-x: -36px;
}
.flag.flag-usa {
  background-position-x: -236px;
}
.flag.flag-japan {
  background-position-x: -436px;
}
```

## If

Stylus has if conditionals that are very useful when it comes to making sure that something has a value and that something is executed if that is met.

```
mixin-box(a, b, margin-only = true)
  if margin-only
    margin: a b
  else
    padding: a b


.div
  mixin-box(10px, 8px, false)
```

Output:

```
.div {
  padding: 10px 8px;
}
```

## You must be interested
* [Try Stylus](http://stylus-lang.com/try.html)


[Try Stylus]: <http://stylus-lang.com/try.html>