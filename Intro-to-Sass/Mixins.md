# Mixins

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
