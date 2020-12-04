# Building the Navigation section

</br>

## TOPICS

- What the "checkbox hack" is, and how it works.

- How to create custom animation timing functions using cubic bezier curves.

- How to animate "solid-color gradients".

- How and why to use *transform-origin*.


</br>


## Checkbox hack

Similar to what we did with the radio button connected to a label, and when the label was clicked, the radio button would become selected.

Only difference here, we are going to use a checkbox instead of a radio button.

**3 steps for this to work:**

1. Make a checkbox, which will be hidden later.

2. Have a label connected to that checkbox, which is where we will click - that will be the button.

3. Reveal the entire navigation in the background when the checkbox is checked.
We can use the *checked* pseudo-class in CSS to style this.


</br>

## Navigation HTML

First element inside the <body> but before the <header>

```
  <!-- Navigation -->
  <div class="navigation">
    <input type="checkbox" class="navigation__checkbox" id="navi-toggle">

    <label for="navi-toggle" class="navigation__button">MENU</label>

    <div class="navigation__background">&nbsp;</div>

    <nav class="navigation__nav">
      <ul class="navigation__list">
        <li class="navigation__item"><a href="#" class="navigation__link">About Natours</a></li>
        <li class="navigation__item"><Your href="#" class="navigation__link">Your benefits</a></li>
        <li class="navigation__item"><a href="#" class="navigation__link">Popular tours</a></li>
        <li class="navigation__item"><a href="#" class="navigation__link">Stories</a></li>
        <li class="navigation__item"><a href="#" class="navigation__link">Book now</a></li>
      </ul>
    </nav>
  </div>
```

</br>

The navigation is part of the **layout**, so that is where we will make the _navigation.scss file, then include it in main.scss.

</br>

### Background

The background for the nav button is basically just a circle.
So, we are creating two circles, one behind and another on top of it.

We also want to give it a background color and have all of those elements' *position: fixed*, and appear in the top right corner.

*position: fixed* iss very similar to *position: absolute* with the difference that with fixed, it **doesn't change position as we scroll the page.**

It also **takes the element out of the flow and allows us to specify it in relation to a positioned element,**
**with the top, left, right, and bottom properties.**


Then we want to use the background-image property, but this time we don't want to use *linear-gradient()*.
Instead, we want to use a **radial-gradient()**, in which colors emerge from a single point and smoothly spread outward in a circular or elliptical shape.


The radial gradient starts in the middle of an element and goes from the middle, outward in all the outside directions.

To prevent this circular nav element from getting hidden, we can add a z-index of a very high value, like 1000.

Inside of _navigation.scss and .navigation {} class
```
&__background {
    height: 6rem;
    width: 6rem;
    border-radius: 50%;
    position: fixed;
    top: 6.5rem;
    right: 6.5rem;
    background-image: radial-gradient($color-primary-light, $color-primary-dark);
    z-index: 1000;
  }
```

Then the larger circle we create will be the .navigation__button
```
&__button {
    background-color: $color-white;
    height: 7rem;
    width: 7rem;
    border-radius: 50%;
    position: fixed;
    top: 6rem;
    right: 6rem;
    z-index: 2000;
  }
```

</br>

Then we want to set the __nav to
```
&__nav {
    height: 100vh;
    width: 100%;
    position: fixed;
    top: 0;
    right: 0;
    z-index: 1500;
  }
```
With its z-index set to a value between the __background and the __button.


### Making the nav button work

We set the transitions on  nav class and the background class,
then add the following selectors to the whole navigation class:
```
  // the checkbox "hack"
  &__checkbox:checked ~ &__background {
    transform: scale(80);
  }
  &__checkbox:checked ~ &__nav {
    opacity: 1;
    width: 100%;
  }
```

</br>

## Custom animation timing functions

**Easing functions** specify the rate of change of a parameter over time.

Objects in real life don’t just start and stop instantly, and almost never move at a constant speed. When we open a drawer, we first move it quickly, and slow it down as it comes out. Drop something on the floor, and it will first accelerate downwards, and then bounce back up after hitting the floor.

[This page helps you choose the right easing function](https://easings.net/)

</br>

### Cubic-bezier function & Easing functions

The **cubic-bezier()** function defines a Cubic Bezier curve.

A Cubic Bezier curve is defined by four points P0, P1, P2, and P3. P0 and P3 are the start and the end of the curve and, in CSS these points are fixed as the coordinates are ratios.
P0 is (0, 0) and represents the initial time and the initial state, P3 is (1, 1) and represents the final time and the final state.

The cubic-bezier() function can be used with the animation-timing-function property and the transition-timing-function property.

- **CSS Syntax:**
```
cubic-bezier(x1,y1,x2,y2)
```
Where the values, x1,y1,x2,y2 are:
**Required. Numeric values. x1 and x2 must be a number from 0 to 1**

</br>

The <easing-function> CSS data type denotes a mathematical function that describes the the rate at which a numerical value changes.

This transition between two values may be applied in different situations. It may be used to describe how fast values change during animations.
This lets you vary the animation's speed over the course of its duration. It may also be used to interpolate between two colors in a color gradient.

The easing functions in the cubic-bezier subset of easing functions are often called "smooth" easing functions, because they can be used to smooth down the start and end of the interpolation.
They correlate an input ratio to an output ratio, both expressed as <number>s. For these values, 0.0 represents the initial state, and 1.0 represents the final state.



Go to [This page for easing functions](https://easings.net/)

Then click which one you want, and copy the values.

</br>

#### The transform-origin property

The transform-origin property allows you to change the position of transformed elements.

2D transformations can change the x- and y-axis of an element. 3D transformations can also change the z-axis of an element.

To better understand the transform-origin property, view a demo.

Note: This property must be used together with the transform property.
