# Mobile-first vs Desktop-first, and Breakpoints

</br>

## Responsive Design Strategies

</br>

#### Desktop-First Strategy

* Start writing CSS for the desktop: large screen.

* Then, write media queries that test for *max-width*, and shrink the design to smaller screens.

</br>

#### Mobile-First Strategy

* Start writing CSS for mobile devices: small screen.

* Then, media queries that test for *min-width* to expand and design to a large desktop screen.

* This forces us to reduce websites and apps to the absolute essentials.

</br>

### Differences between the type of media queries

- Desktop-first: max-width.

For example, we'd write a media query with *max-width: 600px;* as a breakpoint.

So, this breakpoint of 600px is the maximum width at which the media query still applies, and works as expected. After this point it stops working.

The breakpoint could be whatever you feel works best.


**Media queries should be written at the end of your code**
Media queries do not add any importance or specificity to selectors, so code order matters.

</br>

- Mobile-first: min-width.

The mobile first strategy would use the lower end of the pixel size spectrum.
For example, with the initial code having media query with *min-width: 600px;*

This would be the minimum width at which media queries start to apply.

Essentially, this translates to a pixel range starting from 600px and covering all sizes up until infinity.

Screens that have a width larger than 600px will have the code in this media query applied to the page.


</br>

### Mobile-First: Pros and Cons

<br/>

#### PROS:

- 100% optimized for the mobile experience.

- Reduces websites and apps to the absolute essentials.

- Results in smaller, faster, and more efficient products.

- Prioritizes content over aesthetic design, which may be desirable.

</br>

#### CONS:

- The desktop version might feel overly empty and simplistic.

- More difficult and counterintuitive to develop.

- Less creative freedom - making it more difficult to create distinctive products.

- clients are used to see a desktop version of the site as a prototype.

You have to consider if your users are likely to be on their mobile device. So, the purpose of your website will be a main part of choosing the approach.


**NOTE: Either way, you should always keep both the desktop and mobile design approach in mind**

</br>


### Selecting our breakpoints: The Options

**Breakpoints** are the viewport width at which we want our design to change.

In other words, breakpoints are where we want to put our media queries, regardless of which design approach.




- It is bad practice to select breakpoints based on the widths of one popular device for each category.

For example, using only the currently popular Apple products for setting breakpoints to their screen width.
*iPhone -> iPad(mini) -> iPad -> MacBook.*

- It's better to take groupings of all the devices and set breakpoints based on the consideration of the multitude of screen widths.

This would be done, not by setting breakpoints at one specific point, but between similar device width.


- The best approach, in a perfect world, is to ignore devices when selecting breakpoints, and only look at your content and your design.


So, ideally, it works like this:

You begin at one size, either mobile or desktop and then start increasing your screen width or decreasing for desktop first.

Then, as soon as the design breaks, which means that the design no longer works, it no longer looks okay, then you insert a new breakpoint.

So, again, you just put the breakpoints wherever your design starts to look weird and out of place.


The issue here is that this approach can be really difficult, so it's totally acceptable to use the grouping of all popular devices.


