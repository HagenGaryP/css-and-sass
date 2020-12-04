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


