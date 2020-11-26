# Topics

- Thinking about components.

- How and why to use utility classes.

- How to use the *background-clip* property.

- How to *transform* multiple properties simultaneously.

- How to use the *outline-offset* property together with *outline*

- How to style elements that are NOT hovered while others are.


</br>

### Thinking about what we have to build for the About section

There's a heading, which will be an element of the typography.

Under the main heading for this section, we see we are using a grid with two columns - 1 on left, 1 on right.

There are other headings with a paragraph underneath.

So, each of those should go in our typography file.

Then, there is a small secondary button "Learn more" underneath those paragraphs.

On the right side, there is an image composition of 3 total images.
The one you hover over comes to the top, and is gets a green border around the image, while the others become smaller.

The image composition will be treated like a component so we can reuse it.

</br>


### HTML

So we have the header, and now we want to create a **main** element.

The **main** element is just to tell search engines or screen readers that this is really the main part of our site.


So, we have the header, then the main part, which will contain the rest of the website, and then at the end we're also going to have a footer.


</br>

**Emmet extension hot keys**

If you want to write a <div> with the class of "test",
you can just type ".test" and hit TAB, and it will fill out the rest of the html.

If you want to use a different element, you first type the element's name, then ".class-name-here"

For example:

"section.section-about" + TAB
and "h2.heading-secondary" + TAB
gives us the following:
```
<section class="section-about">
    <h2 class="heading-secondary">
        Exciting tours for adventurous people
    </h2>
</section>
```
</br>

#### Effect for the H2 element

The trick is to set the background of the entire H2 element to a **gradient**.

So, we would set the *background-image* property to be a **linear-gradient()**.

A **linear gradient** is created by specifying a straight gradient line, and then several colors placed along that line.

Since we want the color gradient to go from the left to right, we pass **to right** as the first argument for the **linear-gradient()**.
Then pass it the colors.
```
.heading-secondary {
  font-size: 3.5rem;
  text-transform: uppercase;
  font-weight: 700;
  background-image: linear-gradient(to right, $color-primary-light, $color-primary-dark);
  display: inline-block;
}
```
gradient will occupy 100% of available width, since the H2 is a block element.
So, we can change the display prop to inline-block.

**inline-block** - A block box, which itself is flowed as a single inline box, similar to a replaced element.
The inside of an inline-block is formatted as a block box, and the box itself is formatted as an inline box.


#### Block-level Elements
A block-level element always starts on a new line and takes up the full width available (stretches out to the left and right as far as it can).

Here are the block-level elements in HTML:

<address> <article> <aside> <blockquote> <canvas>
<dd> <div> <dl> <dt> <fieldset> <figcaption> <figure>
<footer> <form> (<h1> - <h6>) <header> <hr> <li> <main>
<nav> <noscript> <ol> <p> <pre> <section> <table>
<tfoot> <ul> <video>


#### Inline Elements
An inline element does not start on a new line and it only takes up as much width as necessary.

Here are the inline elements in HTML:

<a> <abbr> <acronym> <b> <bdo> <big> <br> <button>
<cite> <code> <dfn> <em> <i> <img> <input> <kbd>
<label> <map> <object> <output> <q> <samp> <script>
<select> <small> <span> <strong> <sub> <sup>
<textarea> <time> <tt> <var>

Note: An inline element cannot contain a block-level element.

</br>

### The *-webkit-background-clip* property

The next step is making effect happen with the gradient behind the text.


*background-clip* determines the background painting area, but we have to use **-webkit CSS extension**, and set the property to "text"
```
background-clip: text;
-webkit-background-clip: text;
color: transparent;
```

*background-clip* alone will show the gradient without text, since color is set to transparent.

*-webkit-background-clip* will show the value (text) only, with the color gradient applied to the text.


**Setting the color property to "transparent" is what gives the text the colors from the gradient.**

Otherwise, the text just sits on top of the clipped background.
So, this is why we want to make the text invisible by setting *color* to be transparent, letting us see through the text that has a background of the color gradient.

</br>

#### Effect on hover - transforms the H2 with skew()

First add a transition property to the element, so we can control the speed of the skew.

Then inside the **&:hover**, we add the *transform* property and use the **skew()** function

```
&:hover {
    transform: skewY(2deg) skewX(15deg) scale(1.1);
    text-shadow: .5rem 1rem 2rem rgba($color-black, .2);
  }
```

</br>

## Utility classes

Utility classes are very simple classes in CSS, which only have one simple goal.

In our case, the goal is to center the H2 element's text.

So, we will wrap this HTML element in a div with the utility class as followed:
```
<div class="u-center-text">
    <h2 class="heading-secondary">
        Exciting tours for adventurous people
    </h2>
</div>
```

The class starts with the letter **u** to indicate it's a utility class, then you usually add on the goal of the utility to its class property.

The class will be reusable, and this makes it very helpful.

We will style it inside the _utilities.scss file, which is inside the base folder.


```
.u-center-text { text-align: center; }
```

Now the text is centered, because this is a inline block element now.

**Remember we defined the H2 (heading-secondary) as an inline block.**
**So, if we set the parent to *text-align: center;* then that inline block element inside it is treated as text and will therefore be centered in the parent**

</br>


### Using the grid

We can copy the **row** div from the grid in the (commented) markup that we created.

```
<div class="row">
    <div class="col-1-of-2">
        Text content
    </div>
    <div class="col-1-of-2">
        Image composition
    </div>
</div>
```

When adding a margin to the bottom of the H2 element, we can think ahead, since there will probably more than one but could have a different margin-bottom.

So we can just add another utility class to the div that's wrapping the element and style it accordingly.

