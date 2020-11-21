# Three pillars of writing good HTML and CSS

- Responsive Design / Responsive Web Design (RWD)

- Writing maintainable and scalable code

- Web performance

</br>

## Responsive Web Design (RWD)

An approach to web design that makes web pages render well on a variety of devices and window or screen sizes.

Recent work also considers the viewer proximity as part of the viewing context as an extension for RWD.

#### RWD Fundamentals

</br>

[w3schools link](https://www.w3schools.com/css/css_rwd_intro.asp)

</br>

- Fluid Layouts

A **fluid layout** is a type of webpage design in which layout of the page resizes as the window size is changed.
This is accomplished by defining areas of the page using percentages instead of fixed pixel widths.

Most webpage layouts include one, two, or three columns.

- Media Queries (a CSS technique introduced in CSS3)

**Media queries** are a feature of CSS that enable webpage content to adapt to different screen sizes and resolutions.
They are used to customize the appearance of websites for multiple devices.

Media queries may be inserted within a webpage's HTML or included in a separate .CSS file referenced by the webpage.

Example of a simple media query:
```
@media screen and (max-width: 768px)
{
  header { height: 70px; }
  article { font-size: 14px; }
  img { max-width: 480px; }
}
```

The media query above activates if a user's browser window is 768 pixels wide or less.
This could happen if you shrink your window on a desktop computer or if you are using a mobile device, such as a tablet, to view the webpage.

In responsive web design, **media queries act as filters for different screen sizes.**

Like all modules within a cascading style sheet, the ones that appear further down the list override the ones above them.
Therefore, the default styles are typically defined first within a CSS document, followed by the media queries for different screen sizes.
For example, the desktop styles might be defined first, followed by a media query with styles for tablet users, followed by a media query designed for smartphone users.
Styles may also be defined in the opposite order, which is considered "mobile first" development.

- Responsive Images

If the *width* property is set to a percentage and the height is set to "auto", the image will be responsive and scale up and down.
This means the image can be scaled up to be larger than its original size.

A better solution, in many cases, will be to use the *max-width* property instead, also set to 100%.
So, the image will scale down if it has to, but never scale up to be larger than its original size.

**Background images** can also respond to resizing and scaling.

If the *background-size* property is set to "contain", the background image will scale, and try to fit the content area.
However, the image will keep its aspect ratio (the proportional relationship between the image's width and height)

If the *background-size* property is set to "100% 100%", the background image will stretch to cover the entire content area.

If the *background-size* property is set to "cover", the background image will scale to cover the entire content area.
The "cover" value keeps the aspect ratio, so some part of the background image may be clipped.

**Example - Using different images for different devices, with media query.**
```
/* For width smaller than 400px: */
body {
  background-image: url('img_smallflower.jpg');
}

/* For width 400px and larger: */
@media only screen and (min-width: 400px) {
  body {
    background-image: url('img_flowers.jpg');
  }
}
```

You can use the media query *min-device-width*, instead of *min-width*, which checks the device width, instead of the browser width.
Then the image will not change when you resize the browser window.

</br>

## Writing Maintainable and Scalable Code

This essentially means to write code that is:

- Clean

- Easy to understand

- Supports future growth

- Reusable, for you and other developers who might take on your project in the future.

</br>


So, if we want to write maintainable and scalable code, we need to care and think about our **CSS architecture**.

**CSS architecture is the way we organize our files, how we name our classes, and how we structure our mark up in HTML.**

</br>

## Web Performance


Making a website or app more performant means to make it faster and to make it smaller in size, so that the user has to download less data.

Now, there are many things that affect performance, and some factors don't have much to do with our code.
But some of the things that we can do is to make as little HTTP requests as possible.

Meaning that we should include as little as possible files in our HTML document,
write as little code as possible of course, compress our code, and use a preprocessor like Sass.


One of the biggest impact we can have on performance is to reduce the use of images.
This is because images usually makes up the biggest part of the size of a website.

We can do so by using only images that are really necessary for a website or app.
We can also do this by compressing these images so that you use less bandwidth for the final user.
