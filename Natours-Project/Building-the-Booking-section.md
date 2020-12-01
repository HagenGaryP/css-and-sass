# Building the Booking section of the project

</br>

## TOPICS

- How to implement "solid-color gradients"

- How the general and adjacent sibling selectors work, and why we need them.

- How to use the **::input-placeholder** pseudo-element.

- How and when to use the **:focus**, **:invalid**, *placeholder-show*, and **:checked** pseudo-classes.

A reference to all [CSS pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)


- Techniques to build custom radio buttons.


</br>

Here's a [reference for CSS3 gradients](https://css-tricks.com/css3-gradients/)


* Perhaps the most common and useful type of gradient is the *linear-gradient()*.
The gradients “axis” can go from left-to-right, top-to-bottom, or at any angle you chose.
Not declaring an angle will assume top-to-bottom.


You aren’t limited to just two colors either. In fact, you can have as many comma-separated colors as you want.

You can also declare where you want any particular color to “start”.
Those are called **“color-stops”**.
Say you wanted yellow to take up the majority of the space, but red only a little bit in the beginning, you could make the yellow color-stop pretty early:
```
.gradient {
  height: 100px;
  background-color: red;
  background-image:
    linear-gradient(
      to right,
      red,
      yellow 10%
    );
}
```

We tend to think of gradients as fading colors, but if you have two color stops that are the same, you can make a solid color instantly change to another solid color.

This can be useful for declaring a full-height background that simulates columns.
```
.columns-bg {
  background-image:
    linear-gradient(
      to right,
      #fffdc2,
      #fffdc2 15%,
      #d7f0a2 15%,
      #d7f0a2 85%,
      #fffdc2 85%
    );
}
```

</br>

### Making the Solid color gradient on a background-image

By defining the image you want with *background-image: url(../path to image.jpg);*
and adding a linear-gradient, we are able to cover the image with a predefined angle for our gradient.

```
.book {
  background-image: linear-gradient(105deg,
      rgba($color-white, .9) 0%,
      rgba($color-white, .9) 50%,
      transparent 50%),
    url(../img/nat-10.jpg);
  background-size: 100%; // 100% === cover
  border-radius: 3px;
  box-shadow: 0 1.5rem 4rem rgba($color-black, .2);

  // for testing purposes, add height
  height: 50rem;
}
```

This would show the image with the left side (from 0% to 50% of the image), covered in the white color with an opacity of 0.9.
Meaning, the left side of the image is 10% visible.

The first argument passed to the **linear-gradient()** function is the angle.
An angle of 90deg would be straight up and down, slicing the image vertically at the indicated points.
An angle of 180deg would be slicing the image horizontally at the indicated points, with white on top and the bottom being transparent in our case.

The percentages after each of the colors will indicate a start point for the color, and the stop point would be if that same color was used again.





</br>

### Pseudo-classes

A reference to all [CSS pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

</br>

* The **:focus** CSS pseudo-class represents an element (such as a form input) that has received focus.
It is generally triggered when the user clicks or taps on an element or selects it with the keyboard's Tab key.


* The **:invalid** CSS pseudo-class represents any <input> or other <form> element whose contents fail to validate.
```
/* Selects any invalid <input> */
input:invalid {
  background-color: pink;
}
```

* The **:placeholder-shown** CSS pseudo-class represents any <input> or <textarea> element that is currently displaying placeholder text.
```
/* Selects any element with an active placeholder */
:placeholder-shown {
  border: 2px solid silver;
}
```





</br>


### Sibling Selectors

* The general sibling combinator (~) separates two selectors and matches all iterations of the second element, that are following the first element (though not necessarily immediately), and are children of the same parent element.
```
/* Paragraphs that are siblings of and
   subsequent to any image */
img ~ p {
  color: red;
}
```


* The adjacent sibling combinator (+) separates two selectors and matches the second element only if it immediately follows the first element, and both are children of the same parent element.
```
/* Paragraphs that come immediately after any image */
img + p {
  font-weight: bold;
}
```


</br>

Now our _form.scss component looks like this:
```
.form {

  &__group:not(:last-child) {
    margin-bottom: 2rem;
  }

  &__input {
    font-size: 1.5rem;
    // input elements don't automatically inherit the font-family or color like other elements normally would.
    font-family: inherit; // manually inherit font-family
    color: inherit;
    padding: 1.5rem 2rem;
    border-radius: 2px;
    background-color: rgba($color-white, .5);
    border: none;
    border-bottom: 3px solid transparent;
    width: 75%;
    display: block;
    transition: all .3s;

    &:focus {
      outline: none;
      box-shadow: 0 1rem 2rem rgba($color-black, .1);
      border-bottom: 3px solid $color-primary;
    }

    &:focus:invalid {
      border-bottom: 3px solid $color-secondary-dark;
    }

    // PSEUDO-ELEMENT for placeholder
    &::-webkit-input-placeholder {
      color: $color-dark-grey-2
    }
  }

  &__label {
    font-size: 1.2rem;
    font-weight: 700;
    margin-left: 2rem;
    margin-top: .7rem;
    display: block;
    transition: all .3s
  }

  // using the ADJACENT SIBLING SELECTOR +
  &__input:placeholder-shown + &__label {
    opacity: 0; // makes invisible, but element still exists
    visibility: hidden; // this makes hides element.
    transform: translateY(-4rem);
  }

  // hide the radio-input element so only our styled button shows, even though we're using the radio-input element as well
  &__radio-input {
    display: none;
  }

  // form's radio groups displayed side by side
  &__radio-group {
    width: 49%; // any larger and they won't display size by side. This is done instead of using float.
    display: inline-block;
  }

  &__radio-label {
    font-size: $default-font-size;
    cursor: pointer;
    position: relative;
    padding-left: 4.5rem;
  }

  &__radio-button {
    height: 3rem;
    width: 3rem;
    border: 5px solid $color-primary;
    border-radius: 50%;
    // needs to be a block element to work
    display: inline-block;
    // to line up border with radio button, use absolution positioning to its parent radio-label
    position: absolute;
    // set left and top values for positioning
    left: 0;
    top: -.4rem;

    &::after {
      content: "";
      display: block;
      height: 1.3rem;
      width: 1.3rem;
      border-radius: 50%;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: $color-primary;
      opacity: 0;
      transition: opacity .2s;
    }
  }

  // checked radio input / button
  &__radio-input:checked ~ &__radio-label &__radio-button::after {
    opacity: 1;
  }
}
```

We are using the input tag as our radio button, but hiding it so our styled <span> shows and acts like how we wanted.

We still need the <input> for the functionality, but the span is just showing the styling of our choice.

The circle of this <span> has the opacity of zero, until onw of the <input> is checked.  Then it displays the inner circle filled in.
