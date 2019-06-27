# Picture Perfect
A tiny code snippet that enhances the picture HTML element.
Reduce your pages initial load times around 90%, without compromising your users experience.
Let Picture Perfect calculate the srcset and sizes of your images.

[Live demo](https://jsfiddle.net/7hxt3q8b/1/)

## Features
- ✔ Lazy loading.
- ✔ Configurable threshold / viewport offset.
- ✔ Automatic hand picked sizes.
- ✔ Automatic srcset.
- ✔ Automatic srcset with multiple pixel densities.
- ✔ Specify multiple formats.
- ✔ Specify custom media rules.
- ✔ URL string interpolation, gives you control to work on a performance budget.
- ✔ Extends your base sizes and srcset configuration.
- ✔ Art direction, use the native picture features.

## Getting started

Import the snippet into your html file:
```HTML
<script src="main.min.js"></script>
```

Now you can start using the perfect picture:
```HTML
<!--
  Picture Perfect uses <picture> HTML tags to enhance your image delivery.
  You can provide options as HTML attribute for this tag:

  [data-dynamic-url]
    ${format} will be replaced dinamically with the current image format
    ${width} will be replaced dinamically with the current element width
  [data-densities]
    Provide a list of pixel density multipliers comma separated.
    Default : 1
    e.g.: "1,2,3,4" (this will become 1x, 2x, 3x, 4x the current element width)
  [data-automatic-sizes]
    Default: true
    Set to false to disable
  [data-automatic-srcset]
    Default: true
    Set to false to disable
  [proximityThreshold]
    How many pixels before the element gets into the viewport will trigger the lazy loader.
    Default: window.innerHeight/2
    e.g.: "300" (pixels)
    e.g.: "window.innerHeight / 3" (script to eval)
-->
<picture
  data-dynamic-url="https://placehold.it/${width}x${width}.${format}?text=${width}x${width}+${format}"
  data-densities="0.5,1,2,3,4"
  data-automatic-sizes="true"
  data-automatic-srcset="true"
  data-threshold="window.innerHeight / 3"
>

  <!--
    Here you can provide native source HTML elements, use media attributes and define srcset,size and type.
    For each source Picture Perfect will automatically calculate srcset and sizes based on your configuration.
    This allows you to specify multiple file formats and rules to display them.
    You can also add a "data-srcset" attribute, when the element gets close to the viewport the value of this
    attribute will be combined with the true srcset preventing larger images to load on the initial page load.
  -->
  <source srcset="https://placehold.it/50x50.webp?text=50x50+webp" type="image/webp">
  <source srcset="https://placehold.it/50x50.jpg?text=50x50+jpeg" type="image/jpeg">

  <!--
    This next <img> tag is your fallback and hast to be present.
    Add the "make-picture-perfect" attribute to indicate that you want to track this picture/img pair of tags.
  -->
  <img make-picture-perfect alt="fallback" src="https://placehold.it/50x50.jpg">

</picture>
```

## Initializing

#### Just in time

To initialize the plugin you can do it globally at the page load event or one by one for each image
Initializing `PicturePerfect` this way requires you to load the code on the `<head>`.
```HTML
<!-- ONE BY ONE AS THE ELEMENTS GET LOADED (RECOMMENDED) -->
...
  <picture>
    <img onload="JIT_PICTURE_PERFECT(this)" src="myimage.jpg" alt="test-image">
  </picture>
...
```

#### Vanilla javascript at page load

```javascript
// GLOBALLY INITIATED
window.addEventListener('load',function(){
  document.querySelectorAll('picture > img').forEach(PicturePerfect);
});

```

#### jQuery at page load

```javascript
// GLOBALLY INITIATED USING JQUERY
$(document).ready(function(){
  $('picture > img').each(function(){
    new PicturePerfect(this);
  })
})

```

## Support for old browsers

You can use [Picture fill](https://scottjehl.github.io/picturefill/) to support the <picture> tag on older browsers.
