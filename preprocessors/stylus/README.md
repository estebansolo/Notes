# Stylus Course

## Contents
- [Try Stylus Online](#try-stylus-online)
- [Stylus file extensions](#stylus-file-extensions)
- [Import Partials](#import-partials)
- [Variables](#variables)
- [Nesting](#nesting)
- [You must be interested](#you-must-be-interested)

## Try Stylus Online

[Try Stylus]

## Stylus file extensions

In Stylus it is not necessary to use brackets or semicolons.

```stylus
.styl
```
<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Import Partials

One advantage of Sass is the ability to organize our files. We can do this by separating our styles into different files. This way, we no longer have to handle large files, but we can separate them making the job much easier.

Imports can be made in any file, however you must make a main file in order to compile this one file. To import files we use `@import`.

```stylus
@import "_headers.styl"
```

```
file eg: _headers.styl
```

We can import all the files inside a folder

```
@import 'libs/*'
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Variables

Variables are a way of storing the information you want to reuse, you can store different values: colors, fonts, sizes and any value you want to reuse. To create a variable we must assign it a value with the equal sign `=`

```stylus
font-stack = Helvetica, sans-serif
primary-color = #333

body
  font: 100% font-stack
  color: primary-color
```

Output:

```css
body {
	font: 100% Helvetica, sans-serif;
	color: #333;
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Nesting

```stylus
.container, .redtext
  color: red
  > .first-child
    margin-bottom: 20px
  &:before
    content: "Hi"
```

Output:

```css
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

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## You must be interested
* [Try Stylus](http://stylus-lang.com/try.html)

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

[Try Stylus]: <http://stylus-lang.com/try.html>