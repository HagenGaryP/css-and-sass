# BASE FOLDER

The base/ folder holds what we might call the boilerplate code for the project.

In there, you might find the reset file, some typographic rules, and probably a stylesheet defining some standard styles for commonly used HTML elements (that I like to call _base.scss).

_base.scss
_reset.scss
_typography.scss

NOTE: If your project uses a lot of CSS animations, you might consider adding an \_animations.scss file in there containing the **@keyframes** definitions of all your animations.
If you only use a them sporadically, let them live along the selectors that use them.

## Partials

You can create partial Sass files that contain little snippets of CSS that you can include in other Sass files.

This is a great way to modularize your CSS and help keep things easier to maintain.

A partial is a Sass file named with a leading underscore. You might name it something like _partial.scss.

The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file.

Sass partials are used with the **@use** rule.

