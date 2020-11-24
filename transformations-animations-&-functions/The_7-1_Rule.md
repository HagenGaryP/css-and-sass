# Architecture: The 7-1 Pattern

</br>

[The 7-1 pattern: 7 folders, 1 file](https://sass-guidelin.es/#architecture)

Basically, you have all your partials stuffed into 7 different folders, and a single file at the root level (usually named main.scss) which imports them all to be compiled into a CSS stylesheet.

base/
components/
layout/
pages/
themes/
abstracts/
vendors/
And of course:
main.scss

If you are looking to use the 7-1 pattern, there is a [boilerplate](https://github.com/HugoGiraudel/sass-boilerplate) ready on GitHub.
It should contain everything you need to get started with this architecture.

</br>

## BASE FOLDER

The base/ folder holds what we might call the boilerplate code for the project.

In there, you might find the reset file, some typographic rules, and probably a stylesheet defining some standard styles for commonly used HTML elements (that I like to call _base.scss).

_base.scss
_reset.scss
_typography.scss

NOTE: If your project uses a lot of CSS animations, you might consider adding an \_animations.scss file in there containing the **@keyframes** definitions of all your animations.
If you only use a them sporadically, let them live along the selectors that use them.

#### Partials

You can create partial Sass files that contain little snippets of CSS that you can include in other Sass files.

This is a great way to modularize your CSS and help keep things easier to maintain.

A partial is a Sass file named with a leading underscore. You might name it something like _partial.scss.

The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file.

Sass partials are used with the **@use** rule.


</br>


## ABSTRACTS FOLDER

The abstracts/ folder gathers all Sass tools and helpers used across the project.

**Every global variable, function, mixin and placeholder should be put in here.**

The rule of thumb for this folder is that it should not output a single line of CSS when compiled on its own. These are nothing but Sass helpers.

_variables.scss
_mixins.scss
_functions.scss
_placeholders.scss


When working on a very large project with a lot of abstract utilities, it might be interesting to group them by topic rather than type, for instance typography (_typography.scss), theming (_theming.scss), etc.

Each file contains all the related helpers: variables, functions, mixins and placeholders.

Doing so can make the code easier to browse and maintain, especially when files are getting very long.

The abstracts/ folder might also be called utilities/ or helpers/, depending on what you prefer.

- In the abstracts folder, we're only going to put code that's not going to output any css. (i.e., variables, mixins, placeholders, and functions)



</br>


## Layout folder

The layout/ folder contains everything that takes part in laying out the site or application.

This folder could have stylesheets for the main parts of the site (header, footer, navigation, sidebar…), the grid system or even CSS styles for all the forms.

_grid.scss
_header.scss
_footer.scss
_sidebar.scss
_forms.scss
_navigation.scss


NOTE: The layout/ folder might also be called partials/, depending on what you prefer.


</br>

## Components

For smaller components, there is the components/ folder. While layout/ is macro (defining the global wireframe), components/ is more focused on widgets.

It contains all kind of specific modules like a slider, a loader, a widget, and basically anything along those lines.

There are usually a lot of files in components/ since the whole site/application should be mostly composed of tiny modules.

_media.scss
_carousel.scss
_thumbnails.scss

NOTE: The components/ folder might also be called modules/, depending on what you prefer.


### Modules (documentation)

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


</br>

## PAGES FOLDER

If you have page-specific styles, it is better to put them in a pages/ folder, in a file named after the page.

For instance, it’s not uncommon to have very specific styles for the home page hence the need for a _home.scss file in pages/.

_home.scss
_contact.scss


NOTE: Depending on your deployment process, these files could be called on their own to avoid merging them with the others in the resulting stylesheet. It is really up to you.


</br>

## THEMES FOLDER

On large sites and applications, it is not unusual to have different themes.

There are certainly different ways of dealing with themes but I personally like having them all in a themes/ folder.

_theme.scss
_admin.scss


NOTE: This is very project-specific and is likely to be non-existent on many projects.


</br>

## VENDORS FOLDER

And last but not least, most projects will have a vendors/ folder containing all the CSS files from external libraries and frameworks – Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered, and so on.

Putting those aside in the same folder is a good way to say “Hey, this is not from me, not my code, not my responsibility”.

_normalize.scss
_bootstrap.scss
_jquery-ui.scss
_select2.scss


If you have to override a section of any vendor, I recommend you have an 8th folder called *vendors-extensions/* in which you may have files named exactly after the vendors they overwrite.

For instance, *vendors-extensions/_bootstrap.scss* is a file containing all CSS rules intended to re-declare some of Bootstrap’s default CSS.

This is to avoid editing the vendor files themselves, which is generally not a good idea.


</br>


# MAIN FILE

The main file (usually labelled main.scss) should be the only Sass file from the whole code base not to begin with an underscore. This file should not contain anything but @import and comments.

Files should be imported according to the folder they live in, one after the other in the following order:

abstracts/
vendors/
base/
layout/
components/
pages/
themes/
In order to preserve readability, the main file should respect these guidelines:

one file per @import;
one @import per line;
no new line between two imports from the same folder;
a new line after the last import from a folder;
file extensions and leading underscores omitted.
@import 'abstracts/variables';
@import 'abstracts/functions';
@import 'abstracts/mixins';
@import 'abstracts/placeholders';

@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';

@import 'base/reset';
@import 'base/typography';

@import 'layout/navigation';
@import 'layout/grid';
@import 'layout/header';
@import 'layout/footer';
@import 'layout/sidebar';
@import 'layout/forms';

@import 'components/buttons';
@import 'components/carousel';
@import 'components/cover';
@import 'components/dropdown';

@import 'pages/home';
@import 'pages/contact';

@import 'themes/theme';
@import 'themes/admin';
There is another way of importing partials that I deem valid as well. On the bright side, it makes the file more readable. On the other hand, it makes updating it slightly more painful. Anyway, I’ll let you decide which is best, it does not matter much. For this way of doing, the main file should respect these guidelines:

one @import per folder;
a linebreak after @import;
each file on its own line;
a new line after the last import from a folder;
file extensions and leading underscores omitted.
@import
  'abstracts/variables',
  'abstracts/functions',
  'abstracts/mixins',
  'abstracts/placeholders';

@import
  'vendors/bootstrap',
  'vendors/jquery-ui';

@import
  'base/reset',
  'base/typography';

@import
  'layout/navigation',
  'layout/grid',
  'layout/header',
  'layout/footer',
  'layout/sidebar',
  'layout/forms';

@import
  'components/buttons',
  'components/carousel',
  'components/cover',
  'components/dropdown';

@import
  'pages/home',
  'pages/contact';

@import
  'themes/theme',
  'themes/admin';
About Globbing
In computer programming, glob patterns specify sets of filenames with wildcard characters, such as *.scss. To a general extent, globbing means matching a set of files based on an expression instead of a list of filenames. When applied to Sass, it means importing partials into the main file with a glob pattern rather than by listing them individually. This would lead to a main file looking like this:

@import 'abstracts/*';
@import 'vendors/*';
@import 'base/*';
@import 'layout/*';
@import 'components/*';
@import 'pages/*';
@import 'themes/*';
Sass does not support file globbing out of the box because it can be a dangerous feature as CSS is known to be order-dependant. When dynamically importing files (which usually goes in alphabetical order), one does not control the source order anymore, which can lead to hard to debug side-effects.

That being said, in a strict component-based architecture with extra care not to leak any style from one partial to the other, the order should not really matter anymore, which would allow for glob imports. This would make it easier to add or remove partials as carefully updating the main file would no longer be required.

When using Ruby Sass, there is a Ruby gem called sass-globbing that enables exactly that behavior. If running on node-sass, one can rely either on Node.js, or whatever build tool they use to handle the compilation (Gulp, Grunt, etc.).
