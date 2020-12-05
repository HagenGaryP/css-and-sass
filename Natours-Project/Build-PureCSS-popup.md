# Building a pure CSS Popup

</br>

## TOPICS

- How to build a popup with only CSS.

- How to use the *:target* pseudo-class.

- How to create boxes with equal height using *display: table-cell;*.

- How to create CSS text columns.

- How to automatically hyphenate words using *hyphens: auto;* for text.

</br>


### The :target pseudo-class

**The :target CSS pseudo-class represents a unique element (the target element) with an id matching the URL's fragment.**

URLs with an # followed by an anchor name link to a certain element within a document. The element being linked to is the target element.

The :target selector can be used to style the current active target element.


You can use the :target pseudo-class to create a lightbox without using any JavaScript.
This technique relies on the ability of **anchor links** to point to elements that are initially hidden on the page.
Once targeted, the CSS changes their display so that they are shown.

</br>

## Display values - *table* and *table-cell*


***display: table-cell;* elements that are children of a *display: table;* element will behave like they are all in one row.**

You always alter the display property of the element to get the table-style behavior. Here’s the values:
```
display: table                /* <table>     */
display: table-cell           /* <td>        */
display: table-row            /* <tr>        */
display: table-column         /* <col>       */
display: table-column-group   /* <colgroup>  */
display: table-footer-group   /* <tfoot>     */
display: table-header-group   /* <thead>     */
```

There is also display: *inline-table;*
The table elements widths are only as wide as they need to be, yet break onto new lines. It’s almost like they are inline-block elements which happen to break.

***inline-table* makes them literally like inline-block elements, without the breaking.**

</br>

#### The CSS columns Property

Specify the minimum width for each column, and the maximum number of columns:
```
div {
  columns: 100px 3;
}
```

The columns property is a shorthand property for:
*column-width*
*column-count*


The column-width part will define the minimum width for each column, while the column-count part will define the maximum number of columns.
By using this property, the multi-column layout will automatically break down into a single column at narrow browser widths, without the need of media queries or other rules.

</br>

#### CSS Multi-column Properties

**column-count** - Divide the text in a <div> element into three columns:
```
div {
  column-count: 3;
}
```

**column-gap** - Specify a 40 pixels gap between the columns:
```
div {
  column-gap: 40px;
}
```

**column-rule** - Specify the width, style, and color of the rule between columns:
```
div {
  column-rule: 4px double #ff00ff;
}
```

[Reference for CSS Multi-column Properties](https://www.w3schools.com/css/css3_multiple_columns.asp)

The above link has information about each of the properties.

* *column-count*
* *column-gap*
* *column-rule-style*
* *column-rule-width*
* *column-rule-color*
* *column-rule*
* *column-span*
* *column-width*
