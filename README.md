# Orbital
Orbital is a responsive grid framework built with Sass.

With most responsive CSS grid frameworks, your grid has a fixed number of columns, and as the browser window resizes, the size of each column is increased or decreased by the same amount. This time-tested model has strong roots in print design, and works well in many situations. However, there are times where you don't want all of your content to scale down equally. That's where Orbital comes in.

In Orbital, one column is always 50 pixels. As the browser window shrinks or grows, what changes is the number of columns that fit in a single row. This means that different parts of your design can respond differently to changes in resolution: if you want to shrink your main content element while your side navigation bar always stays the same width, Orbital can help you make that happen.

To do this, Orbital defines a number of different breakpoints ('orbitals', if you will) at which the number of columns changes. Currently, there are six different sizes. The names in parentheses are the canonical variable names used in Orbital's API to describe each size.

  * Extra-wide ("wide"): > 1350px
  * Normal ("full"): 1150px-1350px
  * Low-resolution and landscape tablet ("tablet-landscape"): 1000px-1150px
  * Portrait tablet ("tablet-portrait"): 650px-1000px
  * Landscape smartphone ("phone-landscape"): 450px-650px
  * Portrait smartphone ("phone-portrait"): < 450px

When you define an element's width in CSS, you can specify how many columns it should occupy in each of these four sizes, and the elements will resize themselves as appropriate thanks to CSS media queries.

Element widths do cascade. That is to say, if you set a number of columns for a given element, that column size will be applied to all smaller screen sizes unless explicitly set otherwise. Standard CSS selector precedence rules apply here. The one exception is the 'wide' size, which doesn't apply any of its changes to smaller sizes.


## Sass and Semantic Markup
Because Orbital is a Sass library, it doesn't require you to clutter up your HTML with clunky grid framework class names. You can simply apply Orbital's mixins to your pre-existing CSS selectors, letting you keep your markup nice and clean.

Although Orbital is written in Sass, it will work perfectly fine if your code uses the SCSS syntax instead. All examples in this document are using the Sass syntax.

## Usage
Orbital requires Sass 3.2 or newer.

To start using Orbital, simply include _orbital.sass from any Sass/SCSS file.

```@import orbital```

From there, you can access any of its functionality via mixins.

## Demos / Examples

I'm still working on a proper demo page, but for now you can see Orbital live in action on [Lore](http://lore.com) and on my [personal site](http://lazerwalker.com).
The uncompiled Sass stylesheet for my personal site is available on GitHub [here](https://github.com/lazerwalker/lazerwalker.com/blob/master/css/scss/style.sass)

## API Reference
**column**
```
+column($full, $wide, $tablet-landscape, $tablet-portrait, $phone-landscape, $phone-portrait, $subtract, $marginless: true, $table)
```
Sizes the element to a given number of 50px columns.

You must include a value for `$full`. Other than that, all sizes are optional and will default to the `$full` value. As mentioned above, with the exception of the `$wide` size, a value given for a specific screen size will also apply to all smaller screen sizes unless you explicitly set a different value for those smaller screens.

  * `$full`: The number of columns to take up in default view (1150px-1350px)
  * `$wide`: The number of columns for wide view (> 1350px)
  * `$tablet-landscape`: Number of columns for 1000px-1150px
  * `$tablet-portrait`: Number of columns for 650px-1000px
  * `$phone-landscape`: Number of columns for 450px-650px
  * `$phone-portrait`: Number of columns for < 450px
  * `$subtract`: A number of pixels to subtract from the absolute final width. Because all columns are using `box-sizing: border-box`, adding an n-pixel border to an element will cause its internal contents to have 2*n less pixels, which means that children whose column sizes add up to the same as the parent element won't actually fit. By using `$subtract` to shrink the children elements by as many pixels are added by the presence of a border, you can make everything fit.
  * `$marginless`: By default, grid columns do not contain a gutter. If `$marginless` is set to false, a five-pixel gutter will be applied as a left margin.
  * `$table`: Set this to true if the elements being sized are part of an HTML table. By default, columns are arranged horizontally by making them all `float:left`. If the columns are part of a table, this isn't acceptable, so we need to accomodate.

I personally recommend referencing all variables other than $full by name. For example, if you want an element to take up 3 columns on all screen sizes except for a portrait or landscape smartphone, where it should only be 1 column, I would write it as such:

`+column(3, $phone-landscape: 1)`


**full-width-column**
```
+full-width-column($subtract)
```

This is a shorthand function to make an element span the entire width of the page, with an optional subtract value. You can also pass in column numbers for any accepted size (See `+column` definition for variable names), but that isn't recommended.


**before**
```
+before($full, $wide, $tablet-landscape, $tablet-portrait, $phone-landscape, $phone-portrait, $type: 'margin')
```

Adds the given number of columns as whitespace before an element. By default, the whitespace will be added as a margin, but this can be changed to padding by passing in `'padding'` for the `$type` variable


**after**
```
+after($full, $wide, $tablet-landscape, $tablet-portrait, $phone-landscape, $phone-portait, $type: 'margin')
```

Adds the given number of columns as whitespace after an element. As with `+before()`, the whitespace is added as a margin but can be made to use padding.

**media query helpers**
```
  +tablet-landscape
    // Standard Sass/CSS goes here
    border: 1px solid black
    ...
```

For all six screen sizes, there are helper mixins defined to let you easily access the appropriate media query if you need to include any custom styling. They are named appropriately based on the sizes defined above: `+full, +wide, +tablet-landscape, +tablet-portrait, +phone-landscape, +phone-portrait`.

None of the Orbital code uses the mixin for the 'full' size, but it is included in the library for the sake of completeness. If you find yourself using it frequently, that's a likely indicator that your CSS has a bit of code smell and that you might want to reconsider your approach.

## License
Copyright (C) 2012 Lore Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
