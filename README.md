# SFGrid - SCSS Flexbox Grid

**A grid framework and responsive toolkit for SCSS**

## The grid

The grid can be customized in number of columns, vertical gutters and horizontal gutters.
It can be used via SCSS mixins or as utility classes:

### Using the grid in SCSS

````
<div class="contact">
    <div class="contact__image"></div>
    <div class="contact__details"></div>
</div>


.contact {
    @include row();

    &__image, &__details {
        @include col(6);
    }
}
````

### Using the grid with utility classes

````
<div class="contact sfgrid-row">
    <div class="contact__image sfgrid-col-xs-6"></div>
    <div class="contact__details sfgrid-col-xs-6"></div>
</div>
````
ℹ️ The `sfgrid-` prefix can be customized and also be removed.

## The `respond-to()` mixin

`respond-to()` makes it easy to create media queries in your SCSS.

````
.button {
    padding: 20px 40px;

    @include respond-to('md') {
        padding: 30px 60px;
    }
}
````
ℹ️ The names and ranges of your viewport can be customized. By default SFGrid ships the viewport sizes known from Bootstrap.

ℹ️ By default the `respond-to` mixin works "mobile first", that means rules apply for the given viewport and bigger ones. But with the second argument `$direction` you can also declare the rules should apply `only` to this viewport or `down`.

By combining `respond-to()` and `col()` you can easily create responsive grids:

````
.contact {
    @include row();

    &__image, &__details {
        // __image and __details are 12-wide on small screens
        @include col(12);

        @include respond-to('md') {
            // __image and __details are 6-wide and next to each other on medium and bigger screens
            @include col(6);
        }
    }
}
````

## The `grow-linear` mixin

To be documented..

## Reference

### SCSS Variables

|Variable|Description|Default Value|
|---|---|---|
|`$sfgrid-create-grid-classes`|boolean - Only if true the `sfgrid-` utility CSS classes will be generated. Can be switched off if you intend only to use the SCSS mixins|true|
|`$sfgrid-grid-classes-prefix`|string - The `sfgrid-` prefix for the utility CSS classes can be changed with this variable or be set to empty string resulting in classes like `.row` or `.col-md-6`|`sfgrid-`|
|`$sfgrid-columns`|number - Adjusts the number of columns the grid is based on|12|
|`$sfgrid-viewport-sizes`|list - A list with the viewport size names as keys and a nested list of two pixel widths indicating the boundaries of the viewport size. `unlimited` is a special value that means the viewport size is no upper limit.|*Definition of the xs, sm, md, lg and xl viewport sizes. See `_variables.scss` for details.*|
|`$sfgrid-vertical-gutters`|list - A list with viewport size names and corresponding vertical grid gutter values. This works mobile first. There must be a value for the smallest viewport size (`xs` by default). It will apply to bigger viewport sizes if not overridden.|`15px` for `xs` and bigger. `25px` for `lg` and bigger.|
|`$sfgrid-horizontal-gutters`|list - Same as `$sfgrid-vertical-gutters` but horizontally.|Same as `$sfgrid-vertical-gutters`|
|`$sfgrid-container-max-width`|number - Number of pixels maximum with for the container (`@include container()` or `.sfgrid-container`). The use of the container is completely optional. It's designed to use the configured vertical gutter left and right until its defined maximum width. If this behaviour is not what you need you can implement your own container. The grid functionality does not depend on it.|`1280`|

### Mixins

|Mixin|Description|
|---|---|
|`container()`|Makes the element a centered content container using the horizontal gutter left and right to integrate nicely with the grid. Usage is completely optional. You're free to use the grid without the container.|
|`row()`|The starting point for the grid, defining a grid row. The gridded elements inside the row can wrap. E.g. 4 6-wide elements will span two lines in the a single row.
|`col($i)`|Makes the element a gridded element with `$i` indicating the number of columns the element should span. By default (in a 12-column grid) `12` means 100% width in the row, `6` means 50% etc.
|`respond-to($viewport-size, $direction)`|Creates a media query to match the given `$viewport-size`. By default it behaves "mobile first". That means it applies to the given viewport size and all bigger ones. But using the `$direction` parameter you can also set it to one viewport size `only` or `down`.|
|`grow-linear()`|To be documented..|
