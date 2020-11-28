# Building the Tours Section

</br>

## Topics

- How to build a rotating card.

- How to use *perspective* in CSS.

- How to use the *backface-visibility* property.

- Using background blend modes.

- How and when to use *box-decoration-break*.


</br>

### Implementing the Card component

Inside this section, create another row div, and add the following html elements to that row.
```
<div class="col-1-of-3">
    <div class="card">
      card text
    </div>
</div>
```

Then add the _card.scss file, and import it in main.scss.

The rotation (while hovering) is done with the *transform* property being set to the *rotateY()* function.
Because it's rotating about the y-axis.

Remember that whenever you're doing an animation by using the *transform* property on some sort of action like a hover or click/active,
it is best to use the *transition* property on the main part of the element (or parent).

Example - for testing purposes
```
.card {
  background-color: orangered;
  height: 50rem;
  transition: all .8s;

  &:hover {
    transform: rotateY(180deg);
  }
}
```

</br>

### Perspective

When the card rotates, we want it to look like the card is actually moving/rotating toward you.

This is done with *perspective* in CSS, and is **defined on the parent element of the one where the transform is being used**.

The value for *perspective* is usually a very large number of pixels/rem, just try out different values to see which looks best.

So what this means for us is that we should define the *perspective* property on the card class/element,
and then have a child element for the rotation.


Create a class, __side, for the card's other side, and add this to the hover.

In the HTML create the other card side and indicate which is the front and back side of the cards, by adding a modifier to the HTML element's classes.


</br>

The difference between the front and back side is the way they do their rotation.
Since the back side has already been rotated to 180deg,
it needs to be rotated back to 0.

We change the hover to be done only on the front side of the card to stop it from continuously rotating.
So, now when you stop hovering, it rotates back to 0, showing the front side.

</br>

There will be 3 different card backs, so we will add another modifier "card__side--back-1" to the element.

_card.scss file - showing the first card only
```
.card {
  perspective: 150rem;
  // to make perspective work with mozilla firefox, unless it's been integrated into browser already.
  // -moz-perspective: 150rem;
  position: relative;
  height: 50rem; // needs to be added for perspective

  &__side {
    color: #fff;
    font-size: 2rem;

    height: 50rem;
    transition: all 1s ease;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    // hide the back part of an element
    backface-visibility: hidden;
    border-radius: 3px; // rounded corners
    // box-shadow: 0 1.5rem 4rem rgba($color-black, .25);
    // can replace part of box-shadow values with a variable, or replace the entire thing.
    box-shadow: $shadow-default rgba($color-black, .25);

    &--front {
      background-color: $color-white;

    }

    &--back {
      background-color: green;
      // rotateY(180deg) on back to stay on back side
      transform: rotateY(180deg); // stops rotation

      &-1 {
        background-image: linear-gradient(to right bottom, $color-secondary-light, $color-secondary-dark);
      }
    }
  }

  &:hover &__side--front {
    transform: rotateY(-180deg);
  }

  // hovering off of the back side of card brings it to 0, the original position.
  &:hover &__side--back {
    transform: rotateY(0);
  }
}
```

