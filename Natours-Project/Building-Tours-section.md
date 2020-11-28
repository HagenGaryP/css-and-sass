# Building the Tours Section

</br>

## Topics

- How to build a rotating card.

- How to use *perspective* in CSS.

- How to use the *backface-visibility* property.

- Using background blend modes.

- How and when to use *box-decoration-break*.


</br>

### Rotating Card

To create the effect of rotating a card, use one of the **rotate** functions with the *transform* property.

The rotate functions include:

**rotate()** - Specifies a 2D rotation by the angle specified in the parameter about the origin of the element, as defined by the transform-origin property.

**rotate3d()** - Specifies a clockwise 3D rotation by the angle specified in last parameter about the [x,y,z] direction vector described by the first 3 parameters.

**rotateX('angle')** - Specifies a clockwise rotation by the given angle about the X axis.

**rotateY('angle')** - Specifies a clockwise rotation by the given angle about the Y axis.

**rotateZ('angle')** - Specifies a clockwise rotation by the given angle about the Z axis.

</br>


### Perspective

The *perspective* CSS property determines the distance between the z=0 plane and the user in order to give a 3D-positioned element some perspective.

- Syntax
```
/* Keyword value */
perspective: none;

/* <length> values */
perspective: 20px;
perspective: 3.5em;

/* Global values */
perspective: inherit;
perspective: initial;
perspective: unset;
```

</br>

- Values

**none** - Indicates that no perspective transform is to be applied.

**<length>** - A <length> giving the distance from the user to the z=0 plane.
It is used to apply a perspective transform to the element and its content.
If the value is 0 or a negative number, no perspective transform is applied.

</br>

- Description

Each 3D element with z>0 becomes larger; each 3D-element with z<0 becomes smaller.
The strength of the effect is determined by the value of this property.

The parts of the 3D elements that are behind the user —
i.e. their z-axis coordinates are greater than the value of the *perspective* CSS property — are not drawn.

The **vanishing** point is by default placed at the center of the element, but its position can be changed using the *perspective-origin* property.

Using this property with a value different than **0** and **none** creates a new stacking context.
Also, in that case, the object will act as a containing block for *position: fixed* elements that it contains.


### The backface-visibility Property

The *backface-visibility* property **defines whether or not the back face of an element should be visible when facing the user.**

The back face of an element is a mirror image of the front face being displayed.

**This property is useful when an element is rotated. It lets you choose if the user should see the back face or not.**


- Syntax
```
/* Keyword values */
backface-visibility: visible;
backface-visibility: hidden;

/* Global values */
backface-visibility: inherit;
backface-visibility: initial;
backface-visibility: unset;
```

The backface-visibility property is specified as one of the keywords listed below.

- Values

**visible** - The back face is visible when turned towards the user.

**hidden** - The back face is hidden, effectively making the element invisible when turned away from the user.

</br>


## Background-blend and box-decoration-break

</br>

### Styling the card

There are 3 elements on the front side of the card.
Card picture, heading, and details.

HTML inside of the card <div>
```
  <div class="card__side card__side--front">
    <div class="card__picture card__picture--1">
      &nbsp;
    </div>
    <h4 class="card__heading">
      <span class="card__heading-span card__heading-span--1">The Sea Explorer</span>
    </h4>
    <div class="card__details">
      <ul>
        <li>3 day tours</li>
        <li>Up to 30 people</li>
        <li>2 tour guides</li>
        <li>Sleep in cozy hotels</li>
        <li>Difficulty: easy</li>
      </ul>
    </div>
  </div>
```

</br>

#### Background-blend

The *background-blend-mode* property defines the blending mode of each background layer (color and/or image).

It sets how an element's background images should blend with each other and with the element's background color.

Blending modes should be defined in the same order as the *background-image* property.
If the blending modes' and background images' list lengths are not equal, it will be repeated and/or truncated until lengths match.

</br>

#### box-decoration-break

The *box-decoration-break* CSS property specifies how an element's fragments should be rendered when broken across multiple lines, columns, or pages.

The specified value will impact the appearance of the following properties:

background, border, border-image, box-shadow, clip-path, margin, padding.

</br>

- Syntax
```
/* Keyword values */
box-decoration-break: slice;
box-decoration-break: clone;

/* Global values */
box-decoration-break: initial;
box-decoration-break: inherit;
box-decoration-break: unset;
```

The box-decoration-break property is specified as one of the keyword values listed below.

- Values

**slice** - The element is initially rendered as if its box were not fragmented, after which the rendering for this hypothetical box is sliced into pieces for each line/column/page.
Note that the hypothetical box can be different for each fragment since it uses its own height if the break occurs in the inline direction, and its own width if the break occurs in the block direction.

**clone** - Each box fragment is rendered independently with the specified border, padding, and margin wrapping each fragment.
The **border-radius, border-image**, and **box-shadow** are applied to each fragment independently.
The background is also drawn independently for each fragment,
which means that a background image with *background-repeat: no-repeat* may nevertheless repeat multiple times.

</br>

_card.scss file - inside **.card** selector
```
&__picture {
    background-size: cover;
    height: 23rem;
    // blend-mode shows the background image blended in
    background-blend-mode: screen; // different filters

    clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);

    // images from unsplash.com
    &--1 {
      // background-image won't show if we don't implement background-blend-mode property on parent
      background-image: linear-gradient(to right bottom, $color-secondary-light, $color-secondary-dark), url(../img/nat-5.jpg);
    }

    &--2 {
      background-image: url(../img/nat-5.jpg);
    }

    &--3 {
      background-image: url(../img/nat-5.jpg);
    }
  }

  &__heading {
    font-size: 2.8rem;
    font-weight: 300;
    text-transform: uppercase;
    text-align: right;
    color: $color-white;
    position: absolute;
    top: 12rem;
    right: 2rem;
    width: 75%;
  }

  /*
  Instead of nesting &-span inside of &__heading,
  we write a new selector path, &__heading-span
  because it's not really a child of the heading.
  "__heading-span" is a new element, so it's not an element of heading,
  and it's not a modifier of heading either.
  */
  &__heading-span {
    padding: 1rem 1.5rem;
    // treating the lines in the heading as if they're 2 different elements
    // -webkit-box-decoration-break: clone;
    box-decoration-break: clone; // applies same styling

    &--1 {
      background-image: linear-gradient(to right bottom,
        rgba($color-secondary-light, .85),
        rgba($color-secondary-dark, .85));
    }
  }

  &__details {
    padding: 3rem;

    ul {
      list-style: none;
      width: 80%;
      // centering a block element, inside of a block element
      margin: 0 auto;

      li {
        text-align: center;
        font-size: 1.5rem;
        padding: 1rem;

        &:not(:last-child) {
          border-bottom: 1px solid $color-grey-light-2;
        }
      }
    }
  }
```
