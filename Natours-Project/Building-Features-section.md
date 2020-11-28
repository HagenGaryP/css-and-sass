# Building the Features Section

</br>

# Topics

- How to include and use an icon font.

- Another way of creating the "skewed" section" design.

- How and when to use the direct child selector.


</br>

So, in this section we have four columns, each with a box.

When we hover, we have this effect that skews the element.

And then in each of these boxes, we have the four features of this company, and then below that is the text.

On the top center of the box, there's an icon with a gradient, just like the one used for the heading in the "About" section.

</br>

#### Icons

[LINEA: Free Icon sets](https://linea.io/)
Can download all the icon sets for free from linea.io

Unzip the file, inside the folder, _basic directory, we will be using the _ICONFONT directory.
Inside _ICONFONT, we want to copy the "fonts" folder and the "styles.css" and paste them to our project's CSS directory.

Change the "styles.css" file to "icon-font.css" to avoid confusion.

Then link that style sheet to our HTML in the <head> tag.


</br>

icon-font.css file
```
@font-face {
  font-family: "linea-basic-10";
  src:url("fonts/linea-basic-10.eot");
  src:url("fonts/linea-basic-10.eot?#iefix") format("embedded-opentype"),
    url("fonts/linea-basic-10.woff") format("woff"),
    url("fonts/linea-basic-10.ttf") format("truetype"),
    url("fonts/linea-basic-10.svg#linea-basic-10") format("svg");
  font-weight: normal;
  font-style: normal;
}
```

What this does is basically includes all 4 of the basic fonts, and defines the font family.
This is because different browsers can read different font formats.

The majority of the icon-font.css file is just a class for each of the icons that were included in the icon pack.

So, all you have to do is include that class in your element you want to use it (in the HTML).

You can use Linea's html icon reference to see which you want to use.




</br>


### Inside the _home.css file

An example showing the same color gradient for the background image, and skewing it.
```
.section-features {
  padding: 20rem 0;
  background-image: linear-gradient(
    to right bottom,
    rgba($color-primary-light, 0.8),
    rgba($color-primary-dark, 0.8)),
    url(../img/nat-4.jpg);
  background-size: cover;

  transform: skewY(-7deg);
  margin-top: -10rem;

  // direct child selector - for all direct children
  & > * { // .section-features > *
    transform: skewY(7deg); // to correct the negative skew
  }
}
```

- direct child selector **>** is used to skew all the elements back to their normal position.


