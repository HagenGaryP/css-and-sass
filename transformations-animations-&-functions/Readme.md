# Section Overview

- Building the Header

- Creating CSS animations

- Building a complex animated button

<br/>

[Reference for CSS Functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions)

<br/>

## Building the Header

#### Topics covered

- **The best way to perform a basic reset using the universal selector**

- **How to set project-wide font definitions**

- **How to clip parts of elements using clip-path**

<br/>

The **clip-path** property lets you clip an element to a basic shape or to an SVG source.

Note: The clip-path property will replace the deprecated clip property.

<br/>

**The linear-gradient() function** sets a linear gradient as the background image.

To create a linear gradient you must define at least two color stops.
Color stops are the colors you want to render smooth transitions among.
You can also set a starting point and a direction (or an angle) along with the gradient effect.
<br/>
The **url()** CSS function is used to include a file. The parameter is an absolute URL, a relative URL, or a data URI.

The url() function can be passed as a parameter of another CSS functions, like the attr() function.
Depending on the property for which it is a value, the resource sought can be an image, font, or a stylesheet.
The url() functional notation is the value for the <url> data type.

<br/>

#### The easiest way to center anything with the *transform*, *top*, and *left* properties.

<br/>

The **transform** property applies a 2D or 3D transformation to an element.
This property allows you to rotate, scale, move, skew, etc., elements.

You can use the **translate()** method with the transform property to move an element from its current position.

<br/>

## Creating CSS Animations

<br/>

- **How to create CSS animations using *@keyframes* and the *animation* property.**

<br/>

### There are generally two types of animations in CSS.

#### 1) Transition property
The first, which is also the easier of the two, is to just use the **transition** property,
and then change the properties that you want to animate on an event (like hovering over an element).

The transition property is a shorthand property for:

<br/>

- [transition-property](https://www.w3schools.com/cssref/css3_pr_transition-property.asp)

The transition-property property specifies the name of the CSS property the transition effect is for (the transition effect will start when the specified CSS property changes).

Tip: A transition effect could typically occur when a user hover over an element.

<br/>

- [transition-duration](https://www.w3schools.com/cssref/css3_pr_transition-duration.asp)

The transition-duration property specifies how many seconds (s) or milliseconds (ms) a transition effect takes to complete.

<br/>

- [transition-timing-function](https://www.w3schools.com/cssref/css3_pr_transition-timing-function.asp)

The transition-timing-function property specifies the speed curve of the transition effect.

This property allows a transition effect to change speed over its duration.

<br/>

- [transition-delay](https://www.w3schools.com/cssref/css3_pr_transition-delay.asp)

The transition-delay property specifies when the transition effect will start.

The transition-delay value is defined in seconds (s) or milliseconds (ms).


*Note: Always specify the transition-duration property, otherwise the duration is 0s, and the transition will have no effect.*

<br/>

#### 2) @keyframes Rule

<br/>

[@keyframes](https://www.w3schools.com/cssref/css3_pr_animation-keyframes.asp)

The @keyframes rule specifies the animation code. The animation is created by gradually changing from one set of CSS styles to another.
During the animation, you can change the set of CSS styles many times.

Specify when the style change will happen in percent, or with the keywords "from" and "to", which is the same as 0% and 100%.
0% is the beginning of the animation, 100% is when the animation is complete.


Tip: For best browser support, you should always define both the 0% and the 100% selectors.

Note: Use the animation properties to control the appearance of the animation, and also to bind the animation to selectors.

Note: The !important rule is ignored in a keyframe (See last @keyframes example).

<br/>

**CSS Syntax**
```
@keyframes animationname {keyframes-selector {css-styles;}}
```

<br/>

**Property Values**

| **Value**             |             **Description**                                 |
| --------------------- | ----------------------------------------------------------- |
| *animationname*	      | Required. Defines the name of the animation.                |
| *keyframes-selector*	| <br/>Required. Percentage of the animation duration. <br/><br/> Legal values: <br/><br/> 0-100% <br/> from (same as 0%) <br/> to (same as 100%) <br/><br/> **Note:** You can have many keyframes-selectors in one animation. <br/>|
| *css-styles*          |	Required. One or more legal CSS style properties             |


<br/>

## @keyframe Examples

<br/>

#### Example - Add many keyframe selectors in one animation:
```
@keyframes mymove {
  0%   {top: 0px;}
  25%  {top: 200px;}
  50%  {top: 100px;}
  75%  {top: 200px;}
  100% {top: 0px;}
}
```

<br/>

#### Example - Change many CSS styles in one animation:
```
@keyframes mymove {
  0%   {top: 0px; background: red; width: 100px;}
  100% {top: 200px; background: yellow; width: 300px;}
}
```

<br/>

#### Example - Many keyframe selectors with many CSS styles:
```
@keyframes mymove {
  0%   {top: 0px; left: 0px; background: red;}
  25%  {top: 0px; left: 100px; background: blue;}
  50%  {top: 100px; left: 100px; background: yellow;}
  75%  {top: 100px; left: 0px; background: green;}
  100% {top: 0px; left: 0px; background: red;}
}
```

<br/>

#### Example - The !important rule is ignored in a keyframe:
```
@keyframes myexample {
  from {top: 0px;}
  50%  {top: 100px !important;} /* ignored */
  to   {top: 200px;}
}
```

<br/>

