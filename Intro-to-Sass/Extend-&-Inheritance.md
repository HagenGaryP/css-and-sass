# Extend / Inheritance

## Sass @extend Directive

- The **@extend** directive lets you share a set of CSS properties from one selector to another.

- The @extend directive is useful if you have almost identically styled elements that only differ in some small details.

The following Sass example first creates a basic style for buttons (this style will be used for most buttons).
Then, we create one style for a "Report" button and one style for a "Submit" button.
Both "Report" and "Submit" button inherit all the CSS properties from the .button-basic class, through the @extend directive.
In addition, they have their own colors defined:

**SCSS Syntax:**
```
.button-basic  {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  @extend .button-basic;
  background-color: red;
}

.button-submit  {
  @extend .button-basic;
  background-color: green;
  color: white;
}
```

After compilation, the CSS will look like this:


**CSS Output:**
```
.button-basic, .button-report, .button-submit {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  background-color: red;
}

.button-submit  {
  background-color: green;
  color: white;
}
```

By using the @extend directive, you do not need to specify several classes for an element in your HTML code, like this:
```
<button class="button-basic button-report">Report this</button>.
```
You just need to specify .button-report to get both sets of styles.

The @extend directive helps keep your Sass code very DRY.

</br>


### From Sass Documentation

- Using **@extend** lets you share a set of CSS properties from one selector to another. It helps keep your Sass very DRY.

- In our example we're going to create a simple series of messaging for errors, warnings and successes using another feature which goes hand in hand with extend, **placeholder classes**.

- A **placeholder class** is a special type of class that only prints when it is extended, and can help keep your compiled CSS neat and clean.

</br>

Example
```
/* This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

</br>

What the above code does is tells .message, .success, .error, and .warning to behave just like %message-shared.

**That means anywhere that %message-shared shows up, .message, .success, .error, & .warning will too.**

**The magic happens in the generated CSS, where each of these classes will get the same CSS properties as %message-shared.**
This helps you avoid having to write multiple class names on HTML elements.

You can extend most simple CSS selectors in addition to placeholder classes in Sass,
but **using placeholders is the easiest way to make sure you aren't extending a class that's nested elsewhere in your styles, which can result in unintended selectors in your CSS.**

Note that the CSS in %equal-heights isn't generated, because %equal-heights is never extended.

</br>


