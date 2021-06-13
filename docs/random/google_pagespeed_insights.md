# Google PageSpeed Insights

## Above the Fold

The avobe the fold is the visible part of the page in the first load

## Remove Display Blocks

Remove links and scripts tags from the head

## Compress JS and CSS files

Some ways you can compress stylesheets are:

- pre-processors
- postCSS
- webpack
- Webpages: [csscompressor]

## Critical CSS

CSS Critical must go into the html directly. But not all the CSS, only the first screenshot, that is, what the user sees as soon as he enters the web page. There are pages to generate our [Critical CSS](https://jonassebastianohlsson.com/criticalpathcssgenerator/)

## Image Optimization

- [Resize](https://resizeimage.net/)
- [Optimize](https://tinypng.com/)

The PNG and GIF formats are formats without loss of compression.

## Pixel density

Use `srcset`

```html
<img src="images/hero.png" srcset="images/hero.png, image/....png" />
```

## More Resources

- [Lazyload](https://github.com/verlok/lazyload)
- [Performance Optimization](https://www.udacity.com/course/website-performance-optimization--ud884)


[google pagespeed insights]: https://developers.google.com/speed/pagespeed/insights/?hl=es
[csscompressor]: https://csscompressor.com/