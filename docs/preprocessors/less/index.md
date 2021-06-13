# Less Course

## Introduction

```
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

```
@import "_headers.less"
```

The way to name the partials that will be imported is with a `_` at the beginning.

```
file eg: _headers.less
```

## Variables

Variables are a way of storing the information you want to reuse, you can store different values: colors, fonts, sizes and any value you want to reuse. Less uses the `@` symbol to make a string a variable.

```
@font-stack: Helvetica, sans-serif;
@primary-color: #333;

body{
  font: 100% @font-stack;
  color: @primary-color;
}
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

```
.btn {
  display: inline-block;
  color: #FF0000;
}

.btn:hover {
  color: white;
}
```

The wildcard `&` is used to refer to the parent.


## Mixins

The mixins allow to define reusable styles in all the stylesheet, the mixins allow us to receive parameters, this functionality helps us a lot, since with only one mixins we can obtain different outputs with only changing the value of the parameter. The names should have a dot at the beginning `.`

```
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


## Functions

Less has functions that we can use. Some of these functions are very useful such as lightening, darkening or inverting a color.

```
lighten(#ffffff, 25%);
darken(#ffffff, 25%);
desaturate(#ff0000, 50%);
calc(~"50% - 50px");
```

The complete list of functions can be viewed here: [Functions]


## Operator

Less has Operators that we can use, these can be + , - , / , *

```
@padding: 20px;
@small-padding: padding / 2;
@color-x: #FF0000 - #000000;
```


## When

This is similar to `if`

```
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

```
.div {
  width: 100%;
  color: black;
}

.section {
  color: black;
}
```


## You must be interested
* [Try Less](http://lesscss.org/less-preview/)


[Try Less]: <http://lesscss.org/less-preview/>
[Functions]: <http://lesscss.org/functions/>