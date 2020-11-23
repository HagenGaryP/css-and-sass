# Mixins & Functions

Mixins and Functions are written in a similar way, using the **@** symbol followed by either "mixin" or "function", then the name, and finally the declarations block.

Functions use the **@return** keyword to return a value.
```
@function divide($a, $b) {
  @return $a / $b;
}
```

To use this "divide" function for something that requires units like pixels -> call function with args and multiply by 1px;
```
nav {
  margin: divide(60, 2) * 1px;
}
```

This isn't really practical, but it's just an example of how to use functions.

</br>

The **@mixin** directive lets you create CSS code that is to be reused throughout the website.

The **@include** directive is created to let you use (include) the mixin.

- Defining a Mixin with the @mixin directive.

Sass @mixin Syntax::
```
@mixin name {
  property: value;
  property: value;
  ...
}
```

</br>

The following example creates a mixin named "important-text":

**SCSS Syntax:**
```
@mixin important-text {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
}
```

</br>

- Using a Mixin

The **@include** directive is used to include a mixin.

So, to include the important-text mixin created above:

**SCSS Syntax:**
```
.danger {
  @include important-text;
  background-color: green;
}
```

The Sass transpiler will convert the above to normal CSS:

**CSS output:**
```
.danger {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
  background-color: green;
}
```

A mixin can also include other mixins:

**SCSS Syntax:**
```
@mixin special-text {
  @include important-text;
  @include link;
  @include special-border;
}
```

</br>

### Passing Variables to a Mixin

Mixins accept arguments. This way you can pass variables to a mixin.

Here is how to define a mixin with arguments:

**SCSS Syntax:**
```
/* Define mixin with two arguments */
@mixin bordered($color, $width) {
  border: $width solid $color;
}

.myArticle {
  @include bordered(blue, 1px);  // Call mixin with two values
}

.myNotes {
  @include bordered(red, 2px); // Call mixin with two values
}
```

Notice that the arguments are set as variables and then used as the values (color and width) of the border property.


After compilation, the CSS will look like this:

**CSS Output:**
```
.myArticle {
  border: 1px solid blue;
}

.myNotes {
  border: 2px solid red;
}
```

</br>

### Default Values for a Mixin

It is also possible to define default values for mixin variables:

**SCSS Syntax:**
```
@mixin bordered($color: blue, $width: 1px) {
  border: $width solid $color;
}
```

Then, you only need to specify the values that change when you include the mixin:

**SCSS Syntax:**
```
.myTips {
  @include bordered($color: orange);
}
```

</br>

### Using a Mixin For Vendor Prefixes

Another good use of a mixin is for vendor prefixes.

Here is an example for transform:

**SCSS Syntax:**
```
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.myBox {
  @include transform(rotate(20deg));
}
```

After compilation, the CSS will look like this:

**CSS Output:**
```
.myBox {
  -webkit-transform: rotate(20deg);
  -ms-transform: rotate(20deg);
  transform: rotate(20deg);
}
```

</br>




# Mixins - Sass documentation

Some things in CSS are a bit tedious to write, especially with CSS3 and the many vendor prefixes that exist.

A mixin lets you make groups of CSS declarations that you want to reuse throughout your site.

You can even pass in values to make your mixin more flexible.

A good use of a mixin is for vendor prefixes. Here's an example for transform.
**SCSS syntax**
```
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box { @include transform(rotate(30deg)); }
```

**CSS syntax**
```
.box {
  -webkit-transform: rotate(30deg);
  -ms-transform: rotate(30deg);
  transform: rotate(30deg);
}
```

To create a mixin you use the @mixin directive and give it a name. We've named our mixin transform.

We're also using the variable $property inside the parentheses so we can pass in a transform of whatever we want.

After you create your mixin, you can then use it as a CSS declaration starting with @include followed by the name of the mixin.


# Udemy video examples

HTML
```
<nav>
  <ul class="navigation">
    <li> <a href="#">About us</a> </li>
    <li> <a href="#">Pricing</a> </li>
    <li> <a href="#">Contact</a> </li>
  </ul>
  <div class="buttons">
    <a class="btn-main" href="#">Sign up</a>
    <a class="btn-hot" href="#">Get a quote</a>
  </div>
<nav>
```

</br>

**SCSS syntax**
```
* {
  margin: 0;
  padding: 0;
}

// declaring a variable with the $ operator to indicate a variable
$color-primary: #f9ed69; // yellow
$color-secondary: #f08a5d; // orange
$color-tertiary: #b83b5e; // pink
$color-text-dark: #333; // dark grey
$color-text-light: #eee;

$width-button: 150px;

// creating a mixin with @mixin
@mixin clearfix {
  &::after {
    content: "";
    clear: both;
    display: table;
  }
}

// using mixin with an arg passed in to keep DRY principle
@mixin style-link-text($color) {
  text-decoration: none;
  text-transform: uppercase;
  color: $color;
}

nav {
  margin: 30px;
  background-color: $color-primary;

  // including the mixin "clearfix"
  @include clearfix;
}

.navigation {
  list-style: none;
  float: left;

  li {
    display: inline-block;
    margin-left: 30px;

    &:first-child {
      margin: 0;
    }

    a:link {
      // include mixin "style-link-text" with the dark color;
      @include style-link-text($color-text-dark);
    }
  }
}

.buttons {
  float: right;
}

.btn-main:link,
.btn-hot:link {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radius: 100px;
  width: $width-button;
  // include mixin "style-link-text" with light color passed in
  @include style-link-text($color-text-light);
}

.btn-main {
  &:link {
    background-color: $color-secondary;
  }

  &:hover {
    // using built-in functions to make button 15% darker upon hovering
    background-color: darken($color-secondary, 15%);
  }
}

.btn-hot {
  &:link {
    background-color: $color-tertiary;
  }

  &:hover {
    // using built-in functions to make button 10% lighter upon hovering
    background-color: lighten($color-tertiary, 10%);
  }
}
```

</br>

**CSS syntax**

```
* {
  margin: 0;
  padding: 0;
}

nav {
  margin: 30px;
  background-color: #f9ed69;
}
nav::after {
  content: "";
  clear: both;
  display: table;
}

.navigation {
  list-style: none;
  float: left;
}
.navigation li {
  display: inline-block;
  margin-left: 30px;
}
.navigation li:first-child {
  margin: 0;
}
.navigation li a:link {
  text-decoration: none;
  text-transform: uppercase;
  color: #333;
}

.buttons {
  float: right;
}

.btn-main:link,
.btn-hot:link {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radius: 100px;
  width: 150px;
  text-decoration: none;
  text-transform: uppercase;
  color: #eee;
}

.btn-main:link {
  background-color: #f08a5d;
}
.btn-main:hover {
  background-color: #ea5717;
}

.btn-hot:link {
  background-color: #b83b5e;
}
.btn-hot:hover {
  background-color: #cb5b7b;
}

```
