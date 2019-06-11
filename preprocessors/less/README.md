# Less Course

## Contents
- [Introduction](#introduction)
- [Import Partials](#import-partials)
- [Variables](#variables)
- [Nesting](#nesting)
- [Mixins](#mixins)
- [Functions](#functions)
- [Operator](#operator)
- [When](#when)
- [You must be interested](#you-must-be-interested)

## Introduction

```less
.less
```

### Using Less with Node

```
npm install -g less
lessc less_file.less css_file.css
```

[Try Less]

## Import Partials

One advantage of Less is the ability to organize our files. We can do this by separating our styles into different files. This way, we no longer have to handle large files, but we can separate them making the job much easier.

Imports can be made in any file, however you must make a main file in order to compile this one file. To import files we use `@import`.

```less
@import "_headers.less"
```

The way to name the partials that will be imported is with a `_` at the beginning.

```
file eg: _headers.less
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Variables

Variables are a way of storing the information you want to reuse, you can store different values: colors, fonts, sizes and any value you want to reuse. Less uses the `@` symbol to make a string a variable.

```less
@font-stack: Helvetica, sans-serif;
@primary-color: #333;

body{
  font: 100% @font-stack;
  color: @primary-color;
}
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

```less
@color-red: #FF0000;

.btn{
    display: inline-block;
    color: @color-red;
    &:hover{
        color: white;
    }
}
```

Output:

```css
.btn {
  display: inline-block;
  color: #FF0000;
}

.btn:hover {
  color: white;
}
```

The wildcard `&` is used to refer to the parent.

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Mixins

The mixins allow to define reusable styles in all the stylesheet, the mixins allow us to receive parameters, this functionality helps us a lot, since with only one mixins we can obtain different outputs with only changing the value of the parameter. The names should have a dot at the beginning `.`

```less
.max-width(@m-width: 800px){
    max-width: @m-width;
    margin-left: auto;
    margin-right: auto;
}

.container{
    .max-width;
}

.section{
    margin-bottom: 24px;
    .max-width(80vw);
}
```

Output:

```css
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

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Functions

Less has functions that we can use. Some of these functions are very useful such as lightening, darkening or inverting a color.

```less
lighten(#ffffff, 25%);
darken(#ffffff, 25%);
desaturate(#ff0000, 50%);
calc(~"50% - 50px");
```

The complete list of functions can be viewed here: [Functions]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Operator

Less has Operators that we can use, these can be + , - , / , *

```less
@padding: 20px;
@small-padding: padding / 2;
@color-x: #FF0000 - #000000;
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## When

This is similar to `if`

```less
.responsive (@size) when (@size =< 1024px){
    width: 100%;
}

.div{
    .responsive(800px);
    color: black;
}

.section{
    .responsive(1200px);
    color: black;
}
```

Output:

```css
.div {
  width: 100%;
  color: black;
}

.section {
  color: black;
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## You must be interested
* [Try Less](http://lesscss.org/less-preview/)

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

[Try Less]: <http://lesscss.org/less-preview/>
[Functions]: <http://lesscss.org/functions/>