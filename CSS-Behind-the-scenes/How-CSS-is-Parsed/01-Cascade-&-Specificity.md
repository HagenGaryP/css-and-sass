# The Cascade and Specificity

- A quick review of the official terms that we can find in a **CSS Rule**

A rule consists of a **selector** and a **declaration block**

For example:
```
.my-class-selector {
  color: blue;
  text-align: center;
  font-size: 20px;
}
```

We use the **selector** to select one or more HTML elements that we want to style.

Then in the **declaration block**, everything between the curly braces, is where we write the actual styles.

To do so, we can write one or more **declarations** in each declaration block.

Each **declaration** consists of a CSS **property** and its corresponding value, which is the value that we assign to a property.

This value we assign to a property is called the **declared value**.

</br>

## The CSS Parsing Phase & the Cascade

The first step in the parsing phase is to resolve conflicting CSS declarations, which involves the Cascade.

The second step is to process the final CSS values.

</br>

**The Cascade** is the process of combining different stylesheets and resolving conflicts between different CSS rules and declarations.
These conflicts occur when more than one rule applies to a certain element.

</br>

CSS can come from different sources - Author, User, Browser (user agent).

- Author
The most common one is the CSS that we the developers write.
These declarations that we put in our stylesheets are called the **author declarations.**

- User
Another source can be the user declarations, which is CSS coming from the user.
For example, when the user changes the default font size in the browser, that's **user CSS.**

- Browser / User-agent CSS

Browser CSS is the default browser declarations.

For instance, if we put an anchor tag in our HTML for a link and don't style it, this usually will render it with blue text and underlined.

That's called the **user agent CSS**, because it's set by the browser.

</br>

So the cascade combines the CSS declarations coming from all these different sources.

But how does the cascade actually resolve conflicts when more than one rule applies?

It looks at the **importance (weight)**, at the selector **specificity**, and the **source order** of conflicting declarations, in order to determine which one takes precedence


Here's how that works:

First, the cascade starts by giving the conflicting declarations different importance's based on where they are declared.
So, importance is based on the declaration's source.

#### Importance weight

1. The most important declarations are user declarations marked with the important keyword.

2. Next the second most important declarations are the author declarations marked with important.

3. Third, the normal author declarations.

4. User declarations.

5. The default browser declarations are the least important ones.


- Example of using the **!important** keyword
```
.button {
  font-size: 20px;
  color: white;
  background-color: blue !important;
}

#nav .pull-right .button {
  background-color: green;
}
```

The button element has more than one style, but the one with the *!important* keyword takes precedence.
This is because Author *!important* declarations are a higher level of importance than normal Author declarations.

</br>

What happens when conflicting declarations with the same importance?

The Cascade handles this by calculating and comparing the **specificities** of the declaration selectors.

### SPECIFICITY

1. Inline styles (the highest specificity)

2. IDs

3. Classes, pseudo-classes, attributes

4. Elements and pseudo-elements (the least specific / lowest specificity)


To calculate, start at 0, add 1000 for style attribute, add 100 for each ID, add 10 for each attribute, class or pseudo-class, add 1 for each element name or pseudo-element.

Example:
```
A: h1
B: #content h1
C: <div id="content"><h1 style="color: #ffffff">Heading</h1></div>
```
The specificity of A is 1 (one element)
The specificity of B is 101 (one ID reference and one element)
The specificity of C is 1000 (inline styling)

Since 1 < 101 <br 1000, the third rule (C) has a greater level of specificity, and therefore will be applied.

### SOURCE ORDER & SPECIFICITY RULES for Equal specificity:

**the latest rule counts** - If the same rule is written twice into the external style sheet,
then the lower rule in the style sheet is closer to the element to be styled, and therefore will be applied

</br>

**ID selectors have a higher specificity than attribute selectors** - Look at the following three code lines:
```
div#a {background-color: green;}
#a {background-color: yellow;}
div[id=a] {background-color: blue;}
```

the first rule is more specific than the other two, and will be applied.

</br>

**Contextual selectors are more specific than a single element selector** - The embedded style sheet is closer to the element to be styled.

So in the following situation
```
/* From external CSS file: */
#content h1 {background-color: red;}

/* In HTML file: */
<style>
#content h1 {
  background-color: yellow;
}
</style>
```
the latter rule will be applied.

</br>

**A class selector beats any number of element selectors** - a class selector such as .intro beats h1, p, div, etc:

</br>

**The universal selector and inherited values have a specificity of 0** - *, body * and similar have a zero specificity.
Inherited values also have a specificity of 0.


### Cascade and Specificity: What you need to know

- CSS declarations marked with *!important* have the highest priority.

- You should only use *!important* as a last resource.  It's better to use correct specificities - **more maintainable code**
If something doesn't work the way you think it should, then look at your selector specificities and figure out what's going on.
That is always better than just adding *!important*, which may solve the problem in the short term, but will cause more problems in the long term.

- Inline styles will always have priority over styles in external stylesheets.
But keep in mind, using inline styles is not exactly considered best practice.

- If you want to be really specific, use an ID.

- The universal selector * has no specificity value.

- Rely more on **specificity** than on the **order** of selectors. This way, rearranging your CSS code won't cause issues.

- However, you should rely on order when using **3rd-party stylesheets** - always put your author stylesheet last.

