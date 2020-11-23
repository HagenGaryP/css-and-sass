# What is Sass and how does it work?

**Sass is a CSS preprocessor,** an extension of CSS that adds power and elegance to the basic language.

Having a single CSS file with thousands of lines of code, without any reusable pieces or any logic, is difficult to manage.

Sass provides us with features and tools that CSS simply does not have, without changing the fundamental way CSS works.

</br>

Sass is similar to CSS, but written in a Sass file, then uses a Sass compiler to convert the Sass code into CSS.

So, we need to process our Sass code first - that's why it's called a **CSS preprocessor**.

## Main Sass Features

- **Variables:** For reusable values such as colors, font-sizes spacing, etc...

- **Nesting:** To nest selectors inside of one another, allowing us to write less code.

- **Operators:** For mathematical operations directly inside of CSS.

- **Partials & Imports:** Allows us to write CSS in different files and then importing them all into a single file.

Partials and Imports are one of the most important and useful features of Sass.

- **Mixins:** To write reusable pieces of CSS code.

- **Functions:** Similar to mixins, with the difference being that they produce a value that can then be used later.

- **Extends:** To make different selectors inherit declarations that are common to all of them.

- **Control Directives:** For writing complex code using conditionals and loops. (generally is not entirely needed)


## Sass and SCSS

There are two Sass syntaxes, which can cause some confusion.

The original syntax is just called Sass (Sass syntax), like the language itself.

The other syntax is called SCSS (for “Sassy CSS”), and is a superset of CSS3's syntax.
This means that every valid CSS3 stylesheet is valid SCSS as well.

</br>

- Sass syntax is indentation sensitive and doesn't use curly braces or semicolons.

**Example of Sass Syntax**
```
.navigation
  list-style: none
  float: left

  & li
    display: inline-block
    margin-left 30px
```

</br>

- SCSS syntax is more common, as it's even more syntactically similar to CSS.

**Example of SCSS Syntax**
```
.navigation {
  list-style: none;
  float: left;

  & li {
    display: inline-block;
    margin-left 30px;
  }
}
```



- Declare variables with $

Placing the dollar sign, directly followed by the variable name is how variables are declared in SCSS.

- comments are indicated with //

- nesting consolidates the code and is done as you would with most programming languages

- The ampersand symbol, **&** is used to copy the selector path up until that point. Typically used with pseudo-classes.

```
// declaring a variable with the $ operator to indicate a variable
$color-primary: #f9ed69; // yellow
$color-secondary: #f08a5d; // orange
$color-tertiary: #b83b5e; // pink

nav {
  margin: 30px;
  background-color: $color-primary;
}

.navigation {
  list-style: none;

  // Nesting <li> elements by writing the selector inside another selector
  li {
    display: inline-block;
    margin-left: 30px;
    // to format only the first <li> element, use first-child pseudoclass

    // The & (ampersand symbol) writes selector path up until this point.
    &:first-child { // same as ".navigation li:first-child" if not nested
      margin: 0;
    }
  }
}
```


- Note: the *clearfix* method can be used to fix problems caused by float, when child elements are being floated.

This is usually done by creating a class called a *clearfix* and then adding it to that element.
In the example above it would be on the parent, <nav> element, like <nav class="clearfix">

This is used with the *::after* pseudo-element, written immediately AFTER the collapsed element (nav).

This clearfix pseudoelement, that is then going to clear this float. It will do so with the **clear: both;** property.
Also we should set the display to table, **display: table;**.

This fixes this collapsed element. So, instead of writing a separate class, we could simply add it to the nav.

**HTML from example**
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

**SCSS from example (with the *&::after* clearfix nested in nav)**
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

nav {
  margin: 30px;
  background-color: $color-primary;

  // nesting selectors for "clearfix"
  &::after {
    content: "";
    clear: both;
    display: table;
  }
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
      text-decoration: none;
      text-transform: uppercase;
      color: $color-text-dark;
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
  text-decoration: none;
  text-transform: uppercase;
  width: $width-button;
  color: $color-text-light;
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

**COMPILED CSS from above SCSS example**
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
  text-decoration: none;
  text-transform: uppercase;
  width: 150px;
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
