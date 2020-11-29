# Building the Stories section of the project

</br>

### TOPICS

- How to make text flow around shapes with *shape-outside* and *float*.

- How to apply *filter* to images.

- How to create a background video covering an entire section.

- how to use the <video> HTML element.

- How and when to use the *object-fit_ property.


</br>

## Making text flow around shapes with *shape-outside* and *float*


The shape-outside property controls how content will wrap around a floated element’s bounding-box. Typically this is so that text can reflow over a shape such as a circle, ellipse or a polygon:
For example:
```
.element {
  float: left;
  shape-outside: circle(50%);
  width: 200px;
  height: 200px;
}
```

It’s important to note that this property will only work on floated elements for now, although this is likely to change in the future.

The *shape-outside* property can also be manipulated with **transitions or animations**.

</br>

**Values for the *shape-outside* property**

* circle(): for making circular shapes.

* ellipse(): for making elliptical shapes.

* inset(): for making rectangular shapes.

* polygon(): for creating any shape with 3 or more vertices.

* url(): identifies which image should be used to wrap text around.

* initial: the float area is unaffected.

* inherit: inherits shape-outside value from parent.

</br>

The following values identify which reference of **the box model** should be used for positioning the shape within:

* margin-box

* padding-box

* border-box

These values should be appended to the end, for instance:
```
shape-outside: circle(50% at 0 0) padding-box
```
By default the *margin-box* reference will be used.


</br>

So we use the *shape-outside* property to **define where the content floats around the element, in this case, a circle**.

To actually make the element look like that circle, we can use the *clip-path* property.


</br>

#### Without giving the image a width, it will take up the entire space

**Flexible images for responsive web design always need a defined width and/or height**, without exception.


</br>

When using *transform:* with one the **translate functions**, it's usually best to use the same type of translation on hover/click.

So, if you use translate() on the element, use translate() for the hover, instead of translateY() or translateX().

</br>

Sometimes when doing a translation, it can cut off an image or background.

This can usually be fixed with the *backface-visibility* property.

So, whenever we're dealing with animations and translations, if something unexpected happens,
then see if using the *backface-visibility* property will fix the issue by setting it to hidden.


## The *filter* CSS property

[The filter CSS property](https://developer.mozilla.org/en-US/docs/Web/CSS/filter) applies graphical effects like blur or color shift to an element.
Filters are commonly used to adjust the rendering of images, backgrounds, and borders.

Included in the CSS standard are several functions that achieve predefined effects.
You can also reference an SVG filter with a URL to an SVG filter element.

**Syntax**
```
/* URL to SVG filter */
filter: url("filters.svg#filter-id");

/* <filter-function> values */
filter: blur(5px);
filter: brightness(0.4);
filter: contrast(200%);
filter: drop-shadow(16px 16px 20px blue);
filter: grayscale(50%);
filter: hue-rotate(90deg);
filter: invert(75%);
filter: opacity(25%);
filter: saturate(30%);
filter: sepia(60%);

/* Multiple filters */
filter: contrast(175%) brightness(3%);

/* Use no filter */
filter: none;

/* Global values */
filter: inherit;
filter: initial;
filter: unset;
```

</br>

#### Filter functions:

- **blur(px)** -	Applies a blur effect to the image. A larger value will create more blur.
If no value is specified, 0 is used.


- **brightness(%)** -	Adjusts the brightness of the image.
0% will make the image completely black.
100% (1) is default and represents the original image.
Values over 100% will provide brighter results.


- **contrast(%)** -	Adjusts the contrast of the image.
0% will make the image completely black.
100% (1) is default, and represents the original image.
Values over 100% will provide results with more contrast.

- drop-shadow(h-shadow v-shadow blur spread color)  - Applies a drop shadow effect to the image.
[drop-shadow function reference](https://developer.mozilla.org/en-US/docs/Web/CSS/filter-function/drop-shadow())


- **grayscale(%)** -	Converts the image to grayscale.
0% (0) is default and represents the original image.
100% will make the image completely gray (used for black and white images).
Note: Negative values are not allowed.

- **hue-rotate(deg)** -	Applies a hue rotation on the image.
The value defines the number of degrees around the color circle the image samples will be adjusted.
0deg is default, and represents the original image.
Note: Maximum value is 360deg.

- **invert(%)** -	Inverts the samples in the image.
0% (0) is default and represents the original image.
100% will make the image completely inverted.
Note: Negative values are not allowed.

- **opacity(%)** - Sets the opacity level for the image.
The opacity-level describes the transparency-level, where:
0% is completely transparent.
100% (1) is default and represents the original image (no transparency).
Note: Negative values are not allowed.
Tip: This filter is similar to the opacity property.

- **saturate(%)** -	Saturates the image.
0% (0) will make the image completely un-saturated.
100% is default and represents the original image.
Values over 100% provides super-saturated results.
Note: Negative values are not allowed.

- **sepia(%)** -	Converts the image to sepia.
0% (0) is default and represents the original image.
100% will make the image completely sepia.
Note: Negative values are not allowed.

- **url()** - The url() function takes the location of an XML file that specifies an SVG filter, and may include an anchor to a specific filter element.
Example:
```
filter: url(svg-url#element-id);
```

- **initial** - The initial keyword is used to set any CSS property (or HTML element) to its default value.

- **inherit** -	Inherits this property from its parent element.

</br>

</br>

## Background Video - using the HTML <video> element

The <video> tag is used to embed video content in a document, such as a movie clip or other video streams.

instead of using the src attribute inside the video tag,
we use the <source> tag to embed a video file into this video element.

The <video> tag contains one or more <source> tags with different video sources. The browser will choose the first source it supports.

The text between the <video> and </video> tags will only be displayed in browsers that do not support the <video> element.

#### Optional Attributes

| Attribute  | 	Value     |     	Description                                                  |
| ---------- | ---------- | ------------------------------------------------------------------ |
| autoplay	 | autoplay   |	Specifies that the video will start playing as soon as it is ready |
| controls   | controls	  | Specifies that video controls should be displayed (such as a play/pause button etc).|
| height	   | pixels	    | Sets the height of the video player                                |
| loop	     | loop	      | Specifies that the video will start over again, every time it is finished |
| muted 	   | muted	    | Specifies that the audio output of the video should be muted       |
| poster	   | URL	      | Specifies an image to be shown while the video is downloading, or until the user hits the play button|
| preload |	auto, metadata, or none	| Specifies if and how the author thinks the video should be loaded when the page loads |
| src	       | URL	      | Specifies the URL of the video file                                |
| width	     | pixels	    | Sets the width of the video player                                 |
