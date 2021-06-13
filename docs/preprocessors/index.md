# Preprocessors

## Contents

- [Diferencias entre Sass, Stylus y Less](#diferencias-entre-sass-stylus-y-less)
- [Sass](sass/index)
- [Less](less/index)
- [Stylus](stylus/index)
- [BEM](#bem)

## Differences between Sass, Stylus and Less

There are many css preprocessors. Among them we can find:

* `Less` is a very simple preprocessor.
* `Sass` is a very interesting and complete tool thanks to its community.
* `Stylus` is very complete and complex, inspired by SASS

To choose the best preprocessor depends on what we want to achieve with the project. It will depend on the team and the needs we have with the project.

When we work with preprocessors the code must be compiled to transform it into css so that the html pages can understand it.

## BEM

[BEM] — Block Element Modifier
"It's a methodology that helps you to create reusable components and code sharing in front-end development"

```
/* Block */
.btn{
    /* Element */
    .btn__icon{
        /* Element form the Block */
    }

    /* Modifier */
    .btn--warning{
        /* Same properties except visual changes */
    }
}
```

[BEM]: <http://getbem.com/introduction/>