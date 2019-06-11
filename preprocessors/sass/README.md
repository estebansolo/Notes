# Sass Course

## Contents
- [Introduction](#introduction)
- [Import Partials](#import-partials)
- [Variables](#variables)
  - [Escape a variable](#escape-a-variable)
- [Nesting](#nesting)
- [Mixins](#mixins)
  - [Content](#content)
- [Extend](#extend)
- [Functions](#functions)
  - [Create functions](#create-functions)
- [Arrays](#arrays)
- [Each](#each)
- [For](#for)
- [If](#if)
- [You must be interested](#you-must-be-interested)

## Introduction

Sass provide two extensions. [Syntax Documentation]

```sass
.sass or .scss
```

[Try Sass]

## Import Partials

One advantage of Sass is the ability to organize our files. We can do this by separating our styles into different files. This way, we no longer have to handle large files, but we can separate them making the job much easier.

Imports can be made in any file, however you must make a main file in order to compile this one file. To import files we use `@import`.

```sass
@import "headers"
```

The way to name the partials that will be imported is with a `_` at the beginning, however the compiler recognizes the files without having the extension or the `_`.

```
eg: _headers.sass
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Variables

Variables are a way of storing the information you want to reuse, you can store different values: colors, fonts, sizes and any value you want to reuse. Sass uses the `$` symbol to make a string a variable.

```sass
$font-stack: Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
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

### Escape a variable

To escape a variable is used the wildcard `#` in addition to the keys, this is necessary in cases such as, for example, when the variable is surrounded by quotes and if not put the escape the variable would pass as a string of characters.

```sass
$size: 10

div
  content: "#{$size}"
```

Output:

```css
div {
  content: "10";
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Nesting

```sass
.btn
  font-size: 15pt
  &__icon
    font-size: .6em
  &.btn--info
    background-color: white
```

Output:

```css
.btn {
  font-size: 15pt;
}
.btn__icon {
  font-size: 0.6em;
}
.btn.btn--info {
  background-color: white;
}
```

The wildcard `&` is used to refer to the parent.

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Mixins

The mixins allow to define reusable styles in all the stylesheet, these are defined with the directive **@mixin** followed by the name of the mixin, the mixins allow us to receive parameters, this functionality helps us a lot, since with only one mixins we can obtain different outputs with only changing the value of the parameter.

The mixins are included in the style sheets by using **@include** followed by the name of the mixin and optionally by a list of arguments.

```sass
@mixin h1
  h1
    margin: 0
    padding: 0

@mixin heads($size)
  h1
    font-size: $size

  h2
    font-size: $size - 0.5

  h3
    font-size: $size - 0.8

@mixin wrap-width($width: 800px)
    width: $width
    margin: 0 auto

@include h1
.container
  @influde wrap-width(500px)

@include heads(2em)
@media(max-width: 800px)
  @include heads(1em)
```

Output:

```css
h1 {
  margin: 0;
  padding: 0;
}

.container {
  @influde wrap-width(500px);
}

h1 {
  font-size: 2em;
}

h2 {
  font-size: 1.5em;
}

h3 {
  font-size: 1.2em;
}

@media(max-width: 800px) {
  h1 {
    font-size: 1em;
  }

  h2 {
    font-size: 0.5em;
  }

  h3 {
    font-size: 0.2em;
  }
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Content

One of the characteristics of the mixins is the `@content`. This allows us to include a block of content within a mixin.

```sass
@mixin response-to($width)
  @media only screen and (min-width: $width)
    @content

section
  background: blue
  @include response-to(800px)
    background-color: red
```

Output:

```css
section {
  background: blue;
}
@media only screen and (min-width: 800px) {
  section {
    background-color: red;
  }
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Extend

They allow us to create fragments of styles and then inherit them without having to duplicate the code. Extends are declared with the sign of porcetage `%`.

```sass
%btn
  color: white
  width: 50px

.btn-info
  @extend %btn
  background: blue

.btn-success
  @extend %btn
  background: green
```

Output:

```css
.btn-info, .btn-success {
  color: white;
  width: 50px;
}

.btn-info {
  background: blue;
}

.btn-success {
  background: green;
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Functions

Sass has several functions that we can use. Many of these functions are very useful such as lightening, darkening or inverting a color.

```sass
lighten(#ffffff, 25%)
darken(#ffffff, 25%)
invert(#ffffff)
```

The complete list of functions can be viewed here: [Functions]

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

### Create functions

```sass
@function add($num-one, $num-two)
  @return $num-one + $num-two

.div
  padding: add(10px, 5px)
  color: darken(#F0F0F0, 50%)
```

Output:

```css
.div {
  padding: 15px;
  color: #717171;
}

```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Arrays

```sass
$sizes: ( big: 24px, normal: 16px, small: 14px, x-small: 12px )

p
  font-size: map-get($sizes, normal)

small
  color: black
  font-size: map-get($sizes, x-small)
```

Output:

```css
p {
  font-size: 16px;
}

small {
  color: black;
  font-size: 12px;
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## Each

We can make loops the same way we work in any programming language.

```sass
@each $font in (normal, bold, italic)
  .text-#{$font}
    font-weight: $font

$fw : normal, bold, italic
@each $font in ($fw)
  .text-#{$font}
    font-weight: $font
```

Output:

```css
.text-normal {
  font-weight: normal;
}

.text-bold {
  font-weight: bold;
}

.text-italic {
  font-weight: italic;
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## For

We can use this directive in two ways, using `to` or `through`, the difference is the following:

  - **to** => `@for $var from <start> to <end>{ ... }`
  - **through** => `@for $var from <start> through <end>{ ... }`

For Example, if we want to iterate from 1 to 5

```sass
// 1 - 5 runs 4 times
@for $i from 1 to 5
  .class-#{$i}
    &::before
      content: "#{$i}"

// 1 - 5 runs 5 times
@for $i from 1 through 5
  .class-#{$i}
    &:before
      content: "#{$i}"
```

Output:

```css
.class-1::before {
  content: "1";
}

.class-2::before {
  content: "2";
}

.class-3::before {
  content: "3";
}

.class-4::before {
  content: "4";
}

/* Using through */
.class-5:before {
  content: "5";
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## If

```sass
p
  text-color: blue

$background-color : black
@if $background-color == black
  p
    text-color: $background-color
@else
  p
    text-color: white
```

Output:

```css
p {
  text-color: blue;
}

p {
  text-color: black;
}
```

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

## You must be interested
* [SASS Meister](https://www.sassmeister.com/)
* [SASS Documentation](https://sass-lang.com/)
* [SASS Functions](https://sass-lang.com/documentation/functions)

<div align="right">
  <small><a href="#contents">:arrow_up: Up</a></small>
</div>

[Try Sass]: <https://www.sassmeister.com/>
[Syntax Documentation]: <https://sass-lang.com/documentation/syntax>
[Functions]: <https://sass-lang.com/documentation/functions>