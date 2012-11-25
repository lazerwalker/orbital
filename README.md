# Orbital
Orbital is a responsive grid framework built with Sass.

With most responsive CSS grid frameworks, your grid has a fixed number of columns, and as the browser window resizes, the size of each column is increased or decreased by the same amount. This time-tested model has strong roots in print design, and works well in many situations. However, there are times where you don't want all of your content to scale down equally. That's where Orbital comes in.

In Orbital, one column is always 50 pixels. As the browser window shrinks or grows, what changes is the number of columns that fit in a single row. This means that different parts of your design can respond differently to changes in resolution: if you want to shrink your main content element while your side navigation bar always stays the same width, Orbital can help you make that happen.

To do this, Orbital defines a number of different breakpoints ('orbitals', if you will) at which the number of columns changes. Currently, there are six different sizes:

  * Extra-wide (`wide`): > 1350px
  * Normal (`full`): 1150px-1350px
  * Low-resolution and landscape tablet (`ipad-landscape`): 1000px-1150px
  * Portrait tablet (`ipad-portrait`): 650px-1000px
  * Landscape smartphone (`iphone-landscape`): 450px-650px
  * Portrait smartphone (`iphone-portrait`): < 450px

When you define an element's width in CSS, you can specify how many columns it should occupy in each of these four sizes, and the elements will resize themselves as appropriate thanks to CSS media queries.


## Sass and Semantic Markup
Because Orbital is a Sass library, it doesn't require you to clutter up your HTML with clunky grid framework class names. You can simply apply Orbital's mixins to your pre-existing CSS selectors, letting you keep your markup nice and clean.

Although Orbital is written in Sass, it will work perfectly fine if your code uses the SCSS syntax instead. All examples in this document are using the Sass syntax.

## Usage
To set up orbital, simply include _orbital.sass from any Sass/SCSS file.

```@import orbital```

From there, you can access any of its functionality via mixins.


## API Reference
**column**
```
+column($full, $wide, $ipad-landscape, $ipad-portrait, $subtract, $marginless: true, $table)
```
Sizes the element to a given number of 50px columns.

You must include a value for `$full`. Other than that, all sizes are optional and will default to the `$full` value.

  * `$full`: The number of columns to take up in default view (1150px-1350px)
  * `$wide`: The number of columns for wide view (> 1350px)
  * `$ipad-landscape`: Number of columns for 1000px-1150px
  * `$ipad-portrait`: Number of columns for 650px-1000px
  * `$iphone-landscape`: Number of columns for 480px-650px
  * `$iphone-portrait`: Number of columns for < 480px
  * `$subtract`: A number of pixels to subtract from the absolute final width. Because all columns are using box-sizing: border-box, adding an n-pixel border to an element will cause its internal contents to have 2*n less pixels, which means that children whose column sizes add up to the same as the parent element won't actually fit. By using $subtract to shrink the children elements by as many pixels are added by the presence of a border, you can make everything fit.
  * `$marginless`: By default, grid columns do not contain a gutter. If `$marginless` is set to false, a five-pixel gutter will be applied as a left margin.
  * `$table`: Set this to true if the elements being sized are part of an HTML table. By default, columns are arranged horizontally by making them all float:left. If the columns are part of a table, this isn't acceptable, so we need to accomodate.


**full-width-column**
```
+full-width-column($subtract)
```

This is a shorthand function to make an element span the entire width of the page, with an optional subtract value. You can also pass in column numbers for any accepted size (`$full`, `$wide`, `$ipad-landscape`, etc), but that isn't recommended.


**before**
```
+before($full, $wide, $ipad-landscape, $ipad-portrait, $iphone-landscape, $iphone-portrait, $type: 'margin')
```

Adds the given number of columns as whitespace before an element. By default, the whitespace will be added as a margin, but this can be changed to padding by passing in 'padding' for the $type variable


**after**
```
+after($full, $wide, $ipad-landscape, $ipad-portrait, $iphone-landscape, $iphone-portait, $type: 'margin')
```

Adds the given number of columns as whitespace after an element. As with `+before()`, the whitespace is added as a margin but can be made to use padding.

**media query helpers**
```
  +ipad-landscape
    // Standard Sass/CSS goes here
    border: 1px solid black
    ...
```

For all six screen sizes, there are helper mixins defined to let you easily access the appropriate media query if you need to do custom work.

  * `+wide`
  * `+full`
  * `+ipad-landscape`
  * `+ipad-portrait`
  * `+iphone-landscape`
  * `+iphone-portrait`

None of the Orbital code uses use the 'full' mixin, but it is included in the library for the sake of completeness. If you find yourself using it frequently, that's a likely indicator that your CSS has a bit of code smell and that you might want to reconsider your approach.

## License
Copyright (C) 2012 Lore Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.