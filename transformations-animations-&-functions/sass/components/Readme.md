# Components

For smaller components, there is the components/ folder. While layout/ is macro (defining the global wireframe), components/ is more focused on widgets.

It contains all kind of specific modules like a slider, a loader, a widget, and basically anything along those lines.

There are usually a lot of files in components/ since the whole site/application should be mostly composed of tiny modules.

_media.scss
_carousel.scss
_thumbnails.scss

NOTE: The components/ folder might also be called modules/, depending on what you prefer.


## Modules (documentation)

You don't have to write all your Sass in a single file. You can split it up however you want with the **@use** rule.

The **@use** rule loads another Sass file as a module, which means you can refer to its variables, mixins, and functions in your Sass file with a namespace based on the filename.

Using a file will also include the CSS it generates in your compiled output!

**In the _base.scss file**
```
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

**In the styles.scss file**
```
@use 'base';

.inverse {
  background-color: base.$primary-color;
  color: white;
}
```

Notice we're using **@use 'base';** in the styles.scss file.
When you use a file you don't need to include the file extension. Sass is smart and will figure it out for you.
