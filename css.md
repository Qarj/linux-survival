# css

## Stylesheet Link

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="styles.css" />
    </head>
    <body>
        <p>Lorem ipsum dolor sit amet.</p>
        <p>Lorem ipsum dolor sit amet.</p>
    </body>
</html>
```

styles.css

```css
p {
    color: orange;
}
```

## Embedded Styles

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <style>
            p {
                color: orange;
            }
        </style>
    </head>
    <body>
        <p>Lorem ipsum dolor sit amet.</p>
        <p>Lorem ipsum dolor sit amet.</p>
    </body>
</html>
```

Embedded styles override the stylesheet link.

## Inline Styles

```html
<p style="color: blue; font-weight: bold">Lorem ipsum dolor sit amet.</p>
```

Inline styles override all other styles.

## normalize.css

https://necolas.github.io/normalize.css/

Different browsers have different default values for margin and so on.

Make it the first link.

```html
<link rel="stylesheet" href="css/normalize.css" />
```

## CSS Selectors

element

```css
body {
    margin: 10px;
}
```

class

```css
.user {
    margin: 10px;
}
```

id

```css
#user1 {
    margin: 10px;
}
```

attribute

```css
a[target] {
}

a[target='_blank'] {
}
```

attribute contains text

```css
a[href*='google'] {
}
```

attribute starts with text

```css
a[href^='https'] {
}
```

attribute ends with text

```css
a[href$='com'] {
}
```

attribute starts and ends with text

```css
a[href^='https'$='com'] {
}
```

## Relational Selectors

Descentant Selector

```html
<section id="products">
    <p>Lorem ipsum dolor sit amet.</p>
    <article>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
    </article>
</section>
```

Will make all descendent p elements red, not just the immediate children:

```css
#products p {
    color: red;
}
```

Will just make the immediate children red:

```css
#products > p {
    color: red;
}
```

Will make the immediate sibling p element red:

```css
#products + p {
    color: red;
}
```

Will make all general siblings p elements red:

```css
#products ~ p {
    color: red;
}
```

## Pseudo-class Selectors

First child

```css
article :first-child {
    font-size: 145%;
    font-style: italic;
}
```

First of type p element

```css
article p:first-of-type {
    font-size: 145%;
    font-style: italic;
}
```

Last of type p element

```css
article p:last-of-type {
    font-weight: bold;
}
```

Last child

```css
article :last-child {
    font-weight: bold;
}
```

Odds, evens and every third

```css
ul li:nth-child(odd) {
    background-color: #f0f0f0;
}

ul li:nth-child(even) {
    background-color: #773838;
}

ul li:nth-child(3n) {
    font-style: oblique;
}
```

Visited, link, hover, focus

```css
a:visited,
a:link {
    color: dodgerblue;
}

a:hover,
a:focus {
    color: deeppink;
}
```

## Pseudo Elements

```css
p::first-letter {
    font-size: 200%;
    font-weight: bold;
}

p::first-line {
    font-style: italic;
}

::selection {
    background-color: pink;
}

p::before {
    content: '...';
}
p::after {
    content: '...';
    display: block;
}
```

## Selector Specificty

-   id selector is most specific
-   class selector is second most specific
-   tag / class selector is third most specific

So if you target one id, two classes and four tags, the specificity is `124`.

```css
#user1 .users .people h1 h2 h3 p {
    color: green;
}
```

Hover over the selector in vscode and it will show you.

If two selectors have the same specificity, the one that appears later in the CSS file will override the one that appears earlier.

Can use `!important` to override, but don't do it.

```css
h1 {
    color: green !important;
}
```

## Inheritance

```css
p {
    color: dodgerblue;
    border: 1px solid black;
}

strong {
    color: initial;
    border: inherit;
}
```

Typography generally gets inherited. Can be turned off using `initial`.

For properties that are not inherited, use `inherit`.

## Colours

Google `color picker`.

rgb

```css
.box {
    width: 200px;
    height: 250px;
    background-color: rgb(50, 101, 184);
}
```

rgb with alpha channel (0 to 1)

```css
.box {
    width: 200px;
    height: 200px;
    background-color: rgba(50, 101, 184, 0.5);
}
```

hex system does not have alpha channel

```css
.box {
    width: 200px;
    height: 200px;
    background-color: #f5f5f5;
}
```

hsl system - hue, saturation, lightness

```css
.box {
    width: 200px;
    height: 200px;
    background-color: hsl(25, 40%, 80%);
}
```

With the hsl system you start with a base colour then you play with the saturation and lightness.

hsla system - hue, saturation, lightness, alpha channel

```css
.box {
    width: 200px;
    height: 200px;
    background-color: hsla(25, 40%, 80%, 0.5);
}
```

## Linear Gradient

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <div class="box"></div>
    </body>
</html>
```

```css
.box {
    width: 200px;
    height: 200px;
    background: linear-gradient(dodgerblue, yellow);
}
```

```css
.box {
    width: 200px;
    height: 200px;
    background: linear-gradient(to right, dodgerblue, yellow);
}
```

```css
.box {
    width: 200px;
    height: 200px;
    background: linear-gradient(to bottom right, dodgerblue, yellow);
}
```

```css
.box {
    width: 200px;
    height: 200px;
    background: linear-gradient(45deg, dodgerblue, yellow);
}
```

```css
.box {
    width: 200px;
    height: 200px;
    background: linear-gradient(45deg, dodgerblue, yellow 30%);
}
```

```css
.box {
    width: 200px;
    height: 200px;
    background: linear-gradient(45deg, dodgerblue, yellow 30%, orange);
}
```

## Radial Gradient

```css
.box {
    width: 400px;
    height: 200px;
    background: radial-gradient(dodgerblue, yellow 30%, orange);
}
```

```css
.box {
    width: 400px;
    height: 200px;
    background: radial-gradient(circle, dodgerblue, yellow 30%, orange);
}
```

```css
.box {
    width: 400px;
    height: 200px;
    background: radial-gradient(circle at top left, dodgerblue, yellow 30%, orange);
}
```

https://cssgradient.io

## Borders

```css
.box {
    width: 400px;
    height: 200px;
    background: dodgerblue;
    border: 10px solid royalblue;
}
```

```css
.box {
    width: 400px;
    height: 200px;
    background: dodgerblue;
    border: 10px dotted royalblue;
}
```

```css
.box {
    width: 400px;
    height: 200px;
    background: dodgerblue;
    border: 10px dashed royalblue;
}
```

```css
.box {
    width: 400px;
    height: 200px;
    background: dodgerblue;
    border: 10px dashed royalblue;
    border-top: 20px solid royalblue;
}
```

top right bottom left

```css
.box {
    width: 400px;
    height: 200px;
    background: dodgerblue;
    border: 10px dashed royalblue;
    border-width: 10px 20px 30px 5px; /* top right bottom left */
}
```

rounded corners (will apply to any shadow also)

```css
.box {
    width: 400px;
    height: 200px;
    background: dodgerblue;
    border: 10px dashed royalblue;
    border-radius: 30px;
}
```

make a cirlce

```css
.box {
    width: 200px;
    height: 200px;
    background: dodgerblue;
    border: 10px dashed royalblue;
    border-radius: 100%;
}
```

https://css-tricks.com/the-shapes-of-css

## Shadows

```css
.box {
    width: 200px;
    height: 200px;
    background: dodgerblue;
    box-shadow: 10px 10px;
}
```

```css
body {
    margin: 10px;
}

.box {
    width: 200px;
    height: 200px;
    background: dodgerblue;
    box-shadow: -10px 10px;
}
```

Make a softer shadow, and grey

```css
.box {
    width: 200px;
    height: 200px;
    background: dodgerblue;
    box-shadow: 10px 10px 10px grey;
}
```

Suttle grey shadow all around

```css
.box {
    width: 200px;
    height: 200px;
    background: dodgerblue;
    box-shadow: 0 0 30px grey;
}
```

Shadow of heading blends with background

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <div class="box">
            <h1>Heading</h1>
        </div>
    </body>
</html>
```

```css
.box {
    width: 200px;
    height: 200px;
    background: gold;
    box-shadow: 0 0 30px grey;
}

h1 {
    color: white;
    text-shadow: 3px 3px 5px rgba(0, 0, 0, 0.2);
}
```

## Excercise - make a table

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <table>
            <thead>
                <tr>
                    <th>Country</th>
                    <th>OrderID</th>
                    <th>Order Amount</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>USA</td>
                    <td>1001</td>
                    <td>$1,300</td>
                </tr>
                <tr>
                    <td>USA</td>
                    <td>1001</td>
                    <td>$700</td>
                </tr>
                <tr>
                    <td>CA</td>
                    <td>1002</td>
                    <td>$2,000</td>
                </tr>
                <tr>
                    <td>CA</td>
                    <td>1003</td>
                    <td>$1,000</td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <th>Total</th>
                    <th></th>
                    <th>$5,000</th>
                </tr>
            </tfoot>
        </table>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

table,
td,
th {
    border-collapse: collapse;
    padding: 10px;
}

thead,
tfoot {
    background-color: #427fef;
    color: #fff;
    text-align: left;
}

td {
    border-top: 1px solid #c4dcf3;
    border-bottom: 1px solid #c4dcf3;
}

tbody tr:nth-child(odd) {
    background-color: #eef7ff;
}
```

## Box model

margin -> border -> padding -> content

Use margin to space out content to take advantage of margin collapsing.

Padding is used to add space around the content to the border.

content-box is the default box sizing method

-   100px for the content width, 2*20px for the padding, 2*10px for the border = 160px width

```css
.box {
    width: 100px;
    height: 100px;
    background: gold;
    padding: 20px;
    border: 10px solid orange;
    box-sizing: content-box;
}
```

broder-box makes the width and height be calculated from the border

-   So 2*20px for the padding, 2*10px for the border leaves 40px for the content width

```css
.box {
    width: 100px;
    height: 100px;
    background: gold;
    padding: 20px;
    border: 10px solid orange;
    box-sizing: border-box;
}
```

The width and height properties are only applied to block level elements.

## Universal selector Change the default from content-box to border-box

```css
* {
    box-sizing: border-box;
}
```

But does not apply to pseudo elements!

So do this

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```

## Put two boxes beside each other with inline-block

```css
.box {
    width: 100px;
    height: 100px;
    background: gold;
    padding: 20px;
    border: 10px solid orange;
    box-sizing: border-box;
    display: inline-block;
}
```

There will be a space between the boxes with inline-block

```html
<span class="box">Box</span> <span class="box">Box</span>
```

But if you put the two spans right beside each other, the space goes away

```html
<span class="box">Box</span><span class="box">Box</span>
```

## Overflow

If your content is too big for the box, by default it will overflow.

You can choose to hide, or have scroll bars. `auto` is a good option.

```css
.box {
    border: 3px solid gold;
    width: 150px;
    height: 150px;
    overflow: auto;
}
```

## Measurement Units

`px` is absolute

`%` is relative to the container size

`vw` and `vh` are relative to the viewport size

`em` and `rem` are relative to the font size

If you set the width to 10em, that would be 10 times the font size of the element.
If it doesn't have a font size, it inherits it from the parent element.
By default it is 16px for the `html` element.

If you set the height to 95vh, that would be 95% of the viewport height.

`div` elements have a 0 height by default, the height will grow according to content.

If you use `rem` then it is 10x the font size of the root elment.

In `html` element, can set the font-size to `62.5%` which would be 10px be default - easier for making calculations.

## Positioning

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <div class="boxes">
            <div class="box box-one"></div>
            <div class="box box-two"></div>
            <div class="box box-three"></div>
        </div>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

.boxes {
    border: 3px solid lightgrey;
    position: relative;
}

.box {
    width: 5rem;
    height: 5rem;
}

.box-one {
    background-color: gold;
}

.box-two {
    background-color: tomato;
    position: relative;
    left: 4rem;
    bottom: 4rem;
    z-index: -3;
}

.box-three {
    background-color: dodgerblue;
}
```

Set the position to `relative`.

Can use `left` `right` `top` `bottom` to move the container around.

`z-index` defaults to 0, lower numbers make it further away, higher numbers closer.

If you set the `boxes` class to `relative` you can then make `box-two` have
an `absolute` position as follows

```css
.box-two {
    background-color: tomato;
    position: absolute;
    right: 0;
    top: 0;
    z-index: 99999;
}
```

It will be removed from the flow of the page, so `box-three` will move up.

With `fixed` position the container stays in place even on scroll.

## Floating Elements

`parent` elements do not see floated elements.

When we use floats we should `clear` afterwards.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <article class="tweet clearfix">
            <div class="avatar"></div>
            <p>Lorem ipsum dolor sit amet.</p>
        </article>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

.tweet {
    border: 3px solid lightgrey;
}

.clearfix::after {
    content: '';
    display: block;
    clear: both;
}

.avatar {
    width: 5rem;
    height: 5rem;
    background-color: gold;
    float: left;
    margin-right: 0.5rem;
}

.clear {
    clear: both;
}
```

![clearfix](images/clearfix.png)

Use `FlexBox` and `Grid` instead, `Floating Elements` is a legacy approach.

## FlexBox

Used for laying out elements in one direction.

There is a main axis and a cross axis.

It depends on whether you are using `row` or `column` for the `flex-direction`.

Align items with `justify-content` (main axis) and `align-items` (cross axis).

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <div class="container">
            <div class="box">A</div>
            <div class="box">B</div>
            <div class="box">C</div>
        </div>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

.container {
    border: 3px solid lightgrey;
    display: flex;
    flex-direction: row;
    justify-content: center;
}

.box {
    width: 5rem;
    height: 5rem;
    background: gold;
    margin: 1rem;
}
```

![flexbox-center](images/flexbox-center.png)

`justify-content` other options:

-   `space-evenly`
-   `space-around`
-   `space-between`
-   `flex-start`
-   `flex-end`

`align-content` gives control over wrapped content

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <div class="container">
            <div class="box">A</div>
            <div class="box">B</div>
            <div class="box">C</div>
            <div class="box">D</div>
            <div class="box">E</div>
            <div class="box">F</div>
            <div class="box">G</div>
        </div>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

.container {
    border: 3px solid lightgrey;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    align-content: center;
    height: 90vh;
}

.box {
    width: 5rem;
    height: 5rem;
    background: gold;
    margin: 1rem;
}
```

![flexbox-align-content](images/flexbox-align-content.png)

It is also possible to move one of the boxes to a different position.

This will move the box to the top

```css
.box-one {
    align-self: flex-start;
}
```

Size items with

-   `flex-basis`
-   `flex-grow`
-   `flex-shrink`
-   `flex`

Grow the items

```css
flex-grow: 1;
```

Shrink the items

```css
flex-shrink: 1;
```

Assign different numbers to the boxes to control their relative size.

Using `flex` shorthand

```css
flex: 1 1 15rem;
```

1st value will be grow, second value shrink and third value basis.

## Grid

```css
.container {
    display: grid;
    grid-template-rows: repeat(3, 100px);
    grid-template-columns: repeat(2, 100px);
    grid-template: repeat(3, 100px) / repeat(2, 100px);
    border: 3px solid lightgrey;
}
```

longform syntax

```css
grid-template-rows: repeat(3, 100px);
grid-template-columns: repeat(2, 100px);
```

shorthand syntax

```css
grid: repeat(3, 100px) / repeat(2, 100px);
```

aligning items (default is `stretch`)

-   `justify-items` (horizontal)
-   `align-items` (vertical)

aligning content

```css
justify-content: center;
align-content: center;
height: 90vh;
```

Fractions instead of percentages

```css
grid-template: repeat(3, 100px) / 100px 30fr 70fr;
```

`30fr` is 30% of the (remaining) available space, whereas specifying `30%` would be 30% content space.

gap longhand

```css
row-gap: 10px;
column-gap: 10px;
```

gap shorthand

```css
gap: 10px;
```

Placing items with

-   `grid-row`
-   `grid-column`
-   `grid-area` (shorthand)

Make box one span two columns

```css
.box-one {
    grid-column: 1 / span 2;
}
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <main class="container">
            <img src="https://source.unsplash.com/collection/190727/800x600?1" alt="" class="photo" />
            <img src="https://source.unsplash.com/collection/190727/800x600?2" alt="" class="photo big" />
            <img src="https://source.unsplash.com/collection/190727/800x600?3" alt="" class="photo" />
            <img src="https://source.unsplash.com/collection/190727/800x600?4" alt="" class="photo" />
            <img src="https://source.unsplash.com/collection/190727/800x600?5" alt="" class="photo" />
            <img src="https://source.unsplash.com/collection/190727/800x600?6" alt="" class="photo" />
            <img src="https://source.unsplash.com/collection/190727/800x600?7" alt="" class="photo" />
            <img src="https://source.unsplash.com/collection/190727/800x600?8" alt="" class="photo" />
            <img src="https://source.unsplash.com/collection/190727/800x600?9" alt="" class="photo" />
        </main>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

.container {
    display: grid;
    align-items: center;
    justify-content: flex-start;
    gap: 10px;
}

.photo {
    width: 100%;
    object-fit: cover;
    border-radius: 5px;
}

@media screen and (min-width: 768px) {
    .container {
        grid-template: 50fr 50fr / 50fr 50fr;
    }
}

@media screen and (min-width: 1024px) {
    .container {
        grid-template-columns: repeat(3, 1fr);
    }

    .container img:nth-of-type(3) {
        grid-column: 2 / 4;
        grid-row: 1 / 3;
    }
}
```

![grid-spans](images/grid-spans.png)

Using named areas

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <div class="container">
            <div class="box box-one">A</div>
            <div class="box">B</div>
            <div class="box">C</div>
            <div class="box box-four">D</div>
        </div>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

.container {
    display: grid;
    grid-template: 100px auto 100px / 30fr 70fr;
    grid-template-areas:
        'header  header'
        'sidebar main'
        '.       footer';
    row-gap: 10px;
    column-gap: 10px;
    gap: 10px;
    border: 3px solid lightgrey;
    height: 90vh;
}

.box {
    background-color: gold;
}

.box-one {
    grid-area: header;
}

.box-four {
    grid-area: footer;
}
```

![grid-namedAreas](images/grid-namedAreas.png)

## Hiding Elements

Set `display: none;` removes the element entirely including the space it would take.

Set `visibility: hidden;` hides the element but keeps the space it would take.

## Media Queries for Responsive Design

To provide different styles for different screen sizes, use media queries.

Take a mobile first approach, and do media queries for the desktop.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <div class="container">
            <div class="box">
                <p>
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque provident totam id asperiores? Ad
                    sit voluptates dignissimos recusandae. Maiores odit dignissimos veniam, quibusdam est eius non rerum
                    dolorum sunt recusandae.
                </p>
            </div>
            <div class="box">
                <p>
                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Exercitationem voluptatum facere aliquam
                    aperiam rerum quasi atque deserunt harum, sequi dicta commodi totam!
                </p>
            </div>
        </div>
    </body>
</html>
```

```css
body {
    margin: 10px;
}

.container {
    display: flex;
    flex-direction: column;
}

.box {
    background: gold;
    padding: 1rem;
}

.box:nth-of-type(2) {
    background: dodgerblue;
}

@media screen and (min-width: 600px) {
    .container {
        flex-direction: row;
    }
}

@media screen and (min-width: 900px) {
    .container {
        flex-direction: row;
    }
    .box {
        background: greenyellow;
    }
}

@media print {
    body {
        font-size: 12pt;
    }

    .box {
        padding: 0.5cm;
        background: white;
    }
}
```

![responsive1](images/responsive1.png)

![responsive2](images/responsive2.png)

![responsive3](images/responsive3.png)

## Styling fonts

Web safe fonts

```css
body {
    margin: 10px;
    font-family: Arial, Helvetica, sans-serif;
}

h1 {
    font-family: Georgia, 'Times New Roman', Times, serif;
}

p {
    font-weight: 600;
    font-style: italic;
    font-size: 1rem;
    color: #333;
}
```

## Embedding Web Fonts

Free fonts on [Font Squirrel](https://www.fontsquirrel.com)

-   Open Sans

Font formats

-   TTF
-   OTF
-   EOT
-   WOFF
-   WOFF 2.0

WOFF and WOFF 2.0 are compressed versions of the TTF and OTF files.

Use the Webfont Generator feature of Font Squirrel to generate the necessary files.

Then add them to your project.

```css
@font-face {
    font-family: 'opensans';
    src: url('fonts/open-sans/opensans-regular-webfont.woff2') format('woff2'), url('fonts/open-sans/opensans-regular-webfont.woff')
            format('woff');
    font-weight: normal;
    font-style: normal;
}

@font-face {
    font-family: 'opensans';
    src: url('fonts/open-sans/opensans-bold-webfont.woff2') format('woff2'), url('fonts/open-sans/opensans-bold-webfont.woff')
            format('woff');
    font-weight: bold;
    font-style: normal;
}

body {
    margin: 10px;
    font-family: 'opensans', Arial, Helvetica, sans-serif;
}

h1 {
    font-family: Georgia, 'Times New Roman', Times, serif;
}

p {
    font-size: 1rem;
    color: #111;
}
```

Can reduce the font size by removing unneeded characters from the font.
This is the `Expert Mode` on font squirrel.

`font-display` of `optional` is recommended for web fonts.

```css
@font-face {
    font-family: 'opensans';
    src: url('fonts/open-sans/opensans-regular-webfont.woff2') format('woff2'), url('fonts/open-sans/opensans-regular-webfont.woff')
            format('woff');
    font-weight: normal;
    font-style: normal;
    font-display: optional;
}
```

## Font-Services

Lots of free fonts on [Google Web Fonts](https://fonts.google.com).

Paid fonts

-   Adobe Fonts (fonts.adobe.com)
-   fonts.com
-   fontdeck.com

Put the links google gives you in the `<head>` of your HTML before your own stylesheets

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
    href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&family=Roboto:wght@700&display=optional"
    rel="stylesheet"
/>
```

They can then be used by name

```css
body {
    margin: 10px;
    font-family: 'Open Sans', Arial, Helvetica, sans-serif;
}

h1 {
    font-family: Roboto, Arial, Helvetica, sans-serif;
}
```

## System font stack

If you don't care that the fonts are different on different platforms, you can use the system font stack.

These tend to be modern fonts, better than the web safe fonts. But the web page will look different between platforms.

```css
body {
    margin: 10px;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans',
        'Helvetica Neue', sans-serif;
}

h1 {
    font-family: 'Segoe UI';
}

p {
    font-size: 1rem;
    color: #111;
}
```

## Sizing Fonts

Go to [Type Scale](https://type-scale.com/) to help choose the right font sizes.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <h1>Heading 1</h1>
        <h2>Heading 2</h2>
        <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Officia pariatur distinctio quibusdam cum quo rem
            velit delectus officiis? Autem dolor sit recusandae ducimus similique. Deleniti sint laudantium quaerat
            ullam ipsa? Tempore magni adipisci dicta. Vitae laboriosam nemo amet rerum accusamus esse iste. Deserunt
            ipsa, repudiandae aut minus perspiciatis delectus provident animi eos soluta? Odit, laborum quos corrupti
            quaerat aliquid ipsum! Pariatur, nemo! Atque, quis quisquam dolores inventore eius eaque praesentium
            blanditiis maxime nemo repudiandae unde mollitia, saepe nobis est ad dicta exercitationem soluta, vitae
            delectus debitis laudantium facere eveniet neque. Nostrum molestiae provident dignissimos quaerat autem
            rerum cumque cupiditate nesciunt sunt eos eius fuga odit nihil alias placeat quibusdam excepturi consectetur
            enim, quis voluptas vero praesentium! Asperiores dolorem officiis vero? Facilis totam asperiores magnam
            accusamus animi ipsam iusto laudantium dolor, porro error officiis labore minus vel ab sit sint quia
            perferendis harum recusandae provident consequuntur omnis? Quibusdam reiciendis vero provident!
        </p>
    </body>
</html>
```

```css
body {
    margin: 10px;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans',
        'Helvetica Neue', sans-serif;
    font-size: 1rem;
}

h1,
h2,
h3,
h4,
h5,
h6 {
    font-family: Georgia, 'Times New Roman', Times, serif;
}

h1 {
    font-size: 4.209rem;
}

h2 {
    font-size: 3.157rem;
}

@media screen and (min-width: 400px) {
    html {
        font-size: 130%;
    }
}
```

## Vertical Spacing

Law of proximity - objects close to each other are related.

As a rule of thumb, the top margin should be greater than the bottom margin.

```css
h1 {
    margin: 3rem 0 1rem;
}
```

If you don't supply a unit to the `line-height` it will be treated as a multiplier from the font size.

```css
body {
    font-size: 1rem;
    line-height: 1.5;
}
```

## Horizontal Spacing

```css
body {
    letter-spacing: 1px;
    word-spacing: 2px;
}
```

Ideal line length is between 50 - 70 characters.

Set the width of the line to 50 zeros, (is are smaller)

```css
p {
    width: 50ch;
}
```

## Formatting Text

-   text-align
-   text-indent
-   text-decoration
-   text-transform
-   white-space
-   column-\*
-   direction

Select the p elements after the first one and indent

```css
p + p {
    text-indent: 1rem;
}
```

Underline text

```css
p {
    text-decoration: underline;
}
```

Strike through / line through

```css
p {
    text-decoration: line-through;
}
```

Make text uppercase or lowercase, or capitalize first letter of each word

```css
p {
    text-transform: lowercase;
}
```

Turn off line wrap

```css
p {
    white-space: nowrap;
}
```

Truncate text with three dots ... when it is too long

```css
p {
    border: 3px solid gold;
    width: 50ch;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

Multi column text

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <h1>Heading 1</h1>
        <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Officia pariatur distinctio quibusdam cum quo rem
            velit delectus officiis? Autem dolor sit recusandae ducimus similique. Deleniti sint laudantium quaerat
            ullam ipsa? Tempore magni adipisci dicta. Vitae laboriosam nemo amet rerum accusamus esse iste. Deserunt
            ipsa, repudiandae aut minus perspiciatis delectus provident animi eos soluta?
        </p>
        <p>Another paragraph starts here.</p>
        <p>And yet another</p>
    </body>
</html>
```

```css
body {
    margin: 10px;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans',
        'Helvetica Neue', sans-serif;
    font-size: 1rem;
    line-height: 1.5;
}

h1,
h2,
h3,
h4,
h5,
h6 {
    font-family: Georgia, 'Times New Roman', Times, serif;
}

h1 {
    font-size: 4.209rem;
}

h2 {
    font-size: 3.157rem;
}

h1 {
    margin: 3rem 0 1rem;
}

p {
    width: 50ch;
    column-count: 2;
    column-gap: 2rem;
    column-rule: 3px dotted #999;
}

p + p {
    text-indent: 1rem;
}

@media screen and (min-width: 400px) {
    html {
        font-size: 130%;
    }
}
```

![multicolumn](images/multicolumn.png)

Set the text direction to right-to-left

```css
p {
    direction: rtl;
}
```

## Image Types and Formats

WebP format exists. 25% to 35% better compression than JPEG.

## Content Images

For important images, fill out the alt attribute with a good description.

For a decorative image, set the alt attribute to an empty string so the screen reader skips it. If you don't have an alt attribute, the screen reader will read out the image filename.

## Background Images

```css
html {
    font-size: 62.5%;
}

body {
    margin: 10px;
    background: url(../images/bg-paper.jpg);
    background-repeat: no-repeat;
}
```

`background-repeat` common options

-   no-repeat
-   repeat
-   repeat-x
-   repeat-y

reposition the background-image

```css
body {
    margin: 10px;
    background: url(../images/bg-paper.jpg);
    background-repeat: no-repeat;
    background-position: 100px 100px;
}
```

Can set `background-position` to `100% 100px` to push it to the right.

Stretch image

```css
body {
    margin: 10px;
    background: url(../images/bg-paper@2x.jpg);
    background-repeat: no-repeat;
    background-size: 100%, 100vh;
}
```

Content will scroll but not the background with `background-attachment: fixed;`

```css
body {
    margin: 10px;
    background: url(../images/bg-sanfrancisco.jpg);
    background-repeat: no-repeat;
    background-attachment: fixed;
    height: 300vh;
}
```

## CSS Sprites

An optimisation technique. Reduce the number of http requests.

Get nice icons at [Flat Icon](https://www.flaticon.com/)

Search for css sprites generator, use something like [toptal sprite-generator](https://www.toptal.com/developers/css/sprite-generator/) and copy the generated CSS.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <span class="bg-dishes"></span>
        <span class="bg-landing"></span>
        <span class="bg-rocketship"></span>
        <span class="bg-saturn"></span>
        <span class="bg-ufo"></span>
    </body>
</html>
```

```css
html {
    font-size: 62.5%;
}

body {
    margin: 10px;
}

.bg-dishes {
    width: 100px;
    height: 100px;
    background: url(../images/css_sprites.png) -0 -0;
    display: inline-block;
}

.bg-landing {
    width: 100px;
    height: 100px;
    background: url('../images/css_sprites.png') -100px -0;
    display: inline-block;
}

.bg-rocketship {
    width: 100px;
    height: 100px;
    background: url('../images/css_sprites.png') -200px -0;
    display: inline-block;
}

.bg-saturn {
    width: 100px;
    height: 100px;
    background: url('../images/css_sprites.png') -300px -0;
    display: inline-block;
}

.bg-ufo {
    width: 100px;
    height: 100px;
    background: url('../images/css_sprites.png') -400px -0;
    display: inline-block;
}
```

Remember `display` of `inline-block` needed when applying the class to a span.

![css-sprites](images/css-sprites.png)

## Data URLs

An optimisation technique. Embed the image in the html.

Go to [CSS Portal](https://cssportal.com/image-to-data) and upload the image.

[Satellite Dish](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGQAAABkCAYAAABw4pVUAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAFGmlUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4gPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iQWRvYmUgWE1QIENvcmUgNi4wLWMwMDIgNzkuMTY0MzUyLCAyMDIwLzAxLzMwLTE1OjUwOjM4ICAgICAgICAiPiA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPiA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6cGhvdG9zaG9wPSJodHRwOi8vbnMuYWRvYmUuY29tL3Bob3Rvc2hvcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RFdnQ9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZUV2ZW50IyIgeG1wOkNyZWF0b3JUb29sPSJBZG9iZSBQaG90b3Nob3AgMjEuMSAoTWFjaW50b3NoKSIgeG1wOkNyZWF0ZURhdGU9IjIwMjAtMTAtMDdUMDY6NDA6MTgtMDc6MDAiIHhtcDpNb2RpZnlEYXRlPSIyMDIwLTEyLTA2VDEwOjE2OjIxLTA4OjAwIiB4bXA6TWV0YWRhdGFEYXRlPSIyMDIwLTEyLTA2VDEwOjE2OjIxLTA4OjAwIiBkYzpmb3JtYXQ9ImltYWdlL3BuZyIgcGhvdG9zaG9wOkNvbG9yTW9kZT0iMyIgcGhvdG9zaG9wOklDQ1Byb2ZpbGU9InNSR0IgSUVDNjE5NjYtMi4xIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOmMwMzJmYTMxLTUyNjctNDJiZS04ZDE4LTI4MjBjNjU2YzAwZSIgeG1wTU06RG9jdW1lbnRJRD0ieG1wLmRpZDpjMDMyZmEzMS01MjY3LTQyYmUtOGQxOC0yODIwYzY1NmMwMGUiIHhtcE1NOk9yaWdpbmFsRG9jdW1lbnRJRD0ieG1wLmRpZDpjMDMyZmEzMS01MjY3LTQyYmUtOGQxOC0yODIwYzY1NmMwMGUiPiA8eG1wTU06SGlzdG9yeT4gPHJkZjpTZXE+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJjcmVhdGVkIiBzdEV2dDppbnN0YW5jZUlEPSJ4bXAuaWlkOmMwMzJmYTMxLTUyNjctNDJiZS04ZDE4LTI4MjBjNjU2YzAwZSIgc3RFdnQ6d2hlbj0iMjAyMC0xMC0wN1QwNjo0MDoxOC0wNzowMCIgc3RFdnQ6c29mdHdhcmVBZ2VudD0iQWRvYmUgUGhvdG9zaG9wIDIxLjEgKE1hY2ludG9zaCkiLz4gPC9yZGY6U2VxPiA8L3htcE1NOkhpc3Rvcnk+IDwvcmRmOkRlc2NyaXB0aW9uPiA8L3JkZjpSREY+IDwveDp4bXBtZXRhPiA8P3hwYWNrZXQgZW5kPSJyIj8+dNS0wAAALv1JREFUeNrdvXl4nVd17/9Z+x3OqFmyLNnyEDuJncGZyETmiSSQhKGkJAyl9EILlFJuaS50YGh/oRPtpZe2wO+W2zwUyAVCk5QACSEkgSROiZ04iRM7nidJtsYj6YzvtPf9Yx/J8iBbsp2k9H2e/VjWOTrnffd3r+m71l5bjDGcyGtdBR7aCV0R9FW5aP2g+Z094+bGvRO0akPQmML3XdnTmuGZ1hQPFWr88uQWtmcU0XgV9Dyo1YSBrYZFZ0IQCNV9hnwjRAbEQBhAplWojhv8DLjA8Igh6wmJBi2wOxE+2vbXfHDhpwm0gxYXnShEBKeokUTQqTRKC0YLWgtKO0ik8RcO8fB9v871n/7uYZ9xSU8vN6z4BXv6uljctQ3tJueXgvjDw7XaTWNR3KIx2kH6EmXu0Zh/cWrx5jCVJ84azLwxjOPw0nc+d9jPdjnBV9YBbWh/YZAfDUVcgAjteSHtGQoVvKGSphyaZbsdWeYpbncdGCrLaHuGL3eluavRZbfnw6CA4T/zJfhu0KPE/EDHydkZcehKZ8i4EXurVcpJfJLS8qnEmE8pkzwgSn5NKaLkKA91wgEZL3Hm2p2sdWP8rA8pH5oz4DQJtQiGyw4DRcNQyVAKwRHoLZrWneN8Pu/w+Y5Anu7Jm7/xPR5o8kkKAej/ZFAEsU9Dtvy2fMf4faEYjFYkxqCNodn18LLC7mqFUpygBGpK3WwqlULKURd7TWq98l4jQIoBS77zAo9HNfyWPBgD2kAQ258BOvIwLy8Ml4W+ccNA0SAG8r5VSVt3m4u3C/c1p2SHP8KfNnrc3ZgGwX6GvBYzXlSsWLyZS05+kWKlkeaGMYyx31wL07Q3jFyd0cF9VVeRxA6gEbH3V9MJrii601l2VEoESYKjFGEc5qKIn0686Jw2OqJHXwtAOr63iV/8coDWla1wiGgKaA21yILUkIbTMkJXo9A3rukds3/TmLX/FiKz9KfP8e2WtPnimd1yx0kN3O3E9u9f7Ssa7mTRuc/zV7/3WX5492+wYPGOqdc8R6fLVf+uvcUGYtGI6AN0qyCEWuOJ0OGn6a1WMMagPEUY6c7akP52pubcONN3qxP1EH1l7l47SE9n9jBgHFbsoRxAPgUr5inO6hbas0IlhDiBnAdZD0YqdP9ip/n2I5tZNx5wTlMafHe/xL0ql5vA3hYuPecXdJ+0g/WbVjE83sbwWDv9Ix0fGqk2LFLKIDNYOREItSbvOORdh9gYMKBjITdf39C8yFw5Z0BKsxw1+/YvbBjm2j0T0Jiag1kUu+IrIbRm4YwuWDlf8Bwoh1aqGjLgCWwZNmc/uME89/QO812BVGOKKTXxqkhJLQvpGv/t/V9m4YJeRifa8VIxyuETmNkpTgNknP1KSCl7vyOjyW1zBmS8dPQxUYLhMpcZ+ONqfGxe0eSjVSIIE5jfAGcvELqbhFpdRbkKWrL2Zp/vN7/+o026tmfE3Nqchoz36nhjohLC0XZyzaP8/of+kkXNexne27UczEnI7L5RG0NaKTxR6PqfRCHkmszKOQPS4Rx5zHOgzQEf/lGA+DhdIcHalkoIjoJT2uH0TiHjWbASDSkXmrNQDODHz+vvPbbFPCRIU7NvQTmRwAiAGGqjHTTN28vHf+dOzj5t3fxSpYHZSogGlAieEkz97gRBa86YMyBx5sgjyUDF4bMJrJq+0o97IgTCGGoxtOdgVbcwv8H+P4jt9zTU7cjWAXP9vc8nY1sHzVs78pByrEo4YcCIETCLwpHOt6YW7v7G1dfe92OTOCTamROwMm2x1NWsN2cvq1o7qn6clxjuUHUkfAeUnDhQtLaS4Sg4uUNoTMP2EUMlgrQLngNOHgpFeHCDuX9ll3znvE7e05hCF8LZ2xaRg6RLZKVBLtCiVqHlVoXuQQHFViTI4nih/WyZpdQDiTFToBjru/fNGZAwOvIXOcIdoshPPkzOs4AYYx/yROgMMRAl9r+dDZDxhK3DUKgafMfeRy5tbc/GXnPb3nFz5eWL1ZvacqzvLR3h5qchYKAbuFTgdIx5uxE5E6MwCFKfdTFA7NLQWMBPV6lU0rj+0f1vJUKUaCJtUCIkxiouBRvnDEguPdOXQKRpC2M+ODnv1RgWNkBr2v6ccU+sLtcGSoGVjNM6hd1jsKdgUMoafFeBysJYifk/fEW/eOES+Xhbi/yDoyaX//7ZR5M1nrwdR11uMKdpw8UYHDnILgiA0hhlMI4QRymaW/dx+oKt/HTdG+loKx5RNxrAAWpJQmyM1R4GRISUz5NzBiQ+slf0MTE0Tz5DOYKeBljeDKv7Tywg01VLENt/F7cIGVfYWdBEiQUEBEkpdAWefp4v08gb33SR3I4HJpLrgetFOA1tLjOek9VaIfGkwRH7YEpjFGA0JAoJfVQ5japmkFIG/FJ86fJ1+vEN5/m1KIXjBDPeryM2QCwnMc4kL+eAKZmhYNz87zkD4jkz6HYD1Yhbpkt/YqxBPbkFHu890IidiGtSZTt1F8QY6G4SjDhsGICwDISAD5KFc7uf4YK2x267vvPbp+DSmCSyXJJJPaXsSjXGujTKYNBI5EDkoaoppJJGQg9VS0HNR2ruXmmqfQafoOeC1XddvW8Z9/zsZno6d3Ew02bqnpQrMBCF1LTGEUWYgJ8qkF5a++NSTUpzBkTHM07OzQLnTjdqk27v4kbIuRAbSxoeFwJ1ABzAF+v2ViNhXwV2T0BYtCtOXFjZtY2399zLVZ0/45SGDfQ07YEsRCU5d6Li4EyKsjIgCUZpJHEgcpDAR5UzFoTIQ0IPYmdMYR4wwvd1JlznNBT30FYilOQnfpBz3/WGRyj0d/HAK2exoHkfnhcQJ5OSAa4oBoIaY1GEKwpNjDgR1dGVf+dkG76e6gjnTi6WkxlsiOGWw3lTYwGs6oCz58HafdCRndv8m7p9chWIpfAph8JQFfaUYHTcLsa2XMCKzE7esHANN/f8mFXNG1jSuAmVr0ECBKADRbXqgcQ4boJBQ+ygIgcndNCVrFVDoQuxq1Xo9SE8b1T4b7RWV+taagdVN0YJTj5EskEuMmYtE9kVZt88JF3iw2++m9bsBPesP5dy0kBzdoKsFxGahIGgxmAY4ChNog3GOOS82h37hq/+2+KOk46Rfp/B1Vaai+Uwvn6ood2Fczvhid5Z0Bp15tZ397u51UgYrsD2Cegft2qoOavpyfZy3dKXeOuiH3Nd1+O053ZCpmxvIgQTpKiOtqBJEJWAxOAkmFhIJ4KLgSi2qyxxBogqQ8QyodW8f4u9zHeNG/dZ9jNCiwPaRVIJqjkCJ24J4/BFKpmF3kAHkoCJskgt5tff9P2BN5z6cvaetRc1bB5u5ZXRNNuKMelUQGeDJopTsevEP0sS/8Oi2YlKjk6jzfRCXh3GfiRcGmpOP1ygqoBiaCXkpGYYq1lK/RAAnP2+fxDBUAV2TUBvUahUIOfDBe2v8JaOjZzT9jI3LXyEnoYtkBkAlUA1C2GOcLyRRAOi7XBi0OBGMb4J7A3FQBl2Dp3D6sKFPDl6NgMs6nv/qhcuOCP/TNJT+yk+AxArdLKYOErj+BVU4zjieWBMZ2jCp6mlFvr9HRArTDqEkRxmfnGLLA6/dlK47c5P3bKD0mg7a/tbKYRe8K3nz/j8ut75T3RmWStOOQhVjXiWRnVGQJQ5dMK14YwjfW4xhEUNcF4nfOcVaEpZQs1T+72k0SrsGofeEgyUwDVwbls/l/asZ2XzVt6y8OesnPdLSA/YGa01QZAjLi6u0zNWwYkYUCFOUsWXog0W6hJTmFjAowNXsbG8nJ8VruDxocug7EyqtHMfHr/xwXNO4U3nNe7hyvgezgh/yDLvZbyMi3gToHxIWpsDt/QUVW+p398JsWvBKGShMUDevPEys3rxTQx2ZKSxRr65wJWdA9Baevmck0b+6i3/8G76J9L0dBTnlGCbEZBidDhXjjPkCKlVJTYOuaIH/mNv/fkj2FqEXUUYLkMcwcmNY9zY+QLLlu/i2u41XNT1FGR7QdUgzEGllbjWhDYaplggjUiE6ABXRlBubYowKhWzrClcQW/1FJ4rXs7D4zexYcCHkfoT+iC5ENdEkNOUhpLrngsyz7df3nPFN/QfjD/T/wd8Zd7HuaX7HyBogNhtDP3KEwTuMq+/E4kdC8Z4BjTIb6693vQ2DZgNnTdIaxWjBaoZqGSR0eZ1Sxbs4v+/7Qe8/Z9/g77xPPMahwmS4wQkfRiWKzFcfDTJK9RgZSuc0mz4k0eFxgzMT8dcNX8N5694npXNu7mw8zlSjdtAVSD2oNqKnjiJxGgwxkIgGtA4poLDMDgFK6YJmBqsHXoDT4/exI7yKtZNXMaLE+0U64xzhwcrO2CXSqhUExwxiNFT5J6fcyhPlM964snqxrecmb0sl/W3bYoW1IXPnR9kktWm5i1N9XZC5E6pKTDI7zxzHX74iN7c6Epb9RJiBU49SSUampz7SeZx6VVbuC93D+/918t5YW8bp3QMHR8gjjqEk5kfJ5x5NEBEINBwVY/wZ+d/iwvmbebizm00tW0AtwSRC9UmKPYQa1P34w1GNMaAQ4jDOKi94FQhAgKXLaWzeGLkZnZUTmNz6XzWFJYzFNh7a/KgKwVdvs1rJ8bSFo1pqFQO5J1sJGJI5xyGh6KuH6wtrWlb2npRZ2OyGUNDkFGP6yC9NNXXAbGDSYXIaB68BHnvc9fRUnmE7yxF7ctfQ1a6pnS7EXDMiGmYeBQFUjVcet2j/Lx7O5/+lxv50Y4WKqFz7IDIwQScZoWxuaKjBn2DZTi9Ay6+bgskX4LgPCh1WyNMsh8ASVBG46gCyF5wR+t6rpGB4jKeGr2e1aNvpre6ku3lLnZXrTeWc6DFgzbPTr42Bl3P3++PiwwZX3A9IYnNoU6jgUyjw3g1aims4amBy1LvpZXPmGH/VL+3vW4zIhjNgjHIbc9fTUf5MZ5ZgNm9BNqqpxFOEl11I2vYyt50BVP3MHflWDxvmLs+eC8bt83j55sm6Bs+iVy6CPzO3ACJ9CH33zbbWM9V1gYVw8/RGW3BZSeaZpAY0aBkAtQQuINgAsLyYvZVzmJ7eQWrR29gW/ks9lQWsr3soI0tLco5cHLOTn6iOQCAw3rV2kq5q7ApVDlc9KPRwTya8n3tb+n5Pz+i4iivrx0SB5OOkJEsOBq5/YXL6Sw9YUZymLWLoa2IIJdj3P2fawwi8hjKOXDFDs8j7Yecs3Iv55z3T+CVQbtzB8R3DiIUE5oCPXsmVxkIRTHhvJ/W+GMoJwQZAhnHVLsYLC6nt3o1z41dwdOjN9BbaWM4gJqGjIKsgqU5MNpKQWLmmK6dIvNmel1TLbTRlh1i3bsuoCfd70Qvr8JJFCYVWQMuIO9cfw2dpScA5OeLkVAgrztN1b/xgMyhgFH6x4eoD5VA7MBYzo7DaKBZAVI7lDrJzIlWF+vSBu71TNQuISq9yGhyHesKF/P0yA3sqixgNLSSlHctAN0Zu9KS+urX+vg5MXM4Vaw0tZFW8plxfvHOS+lp7CdefxqiwTiCikKkczNcE1xNE48B8NJ82N4OnUVI1MVoSR2UytWI3mFt4rHzRu5sHwRIHwt1nvOgz/1H7nxRsa+WJQJSYlVQmw/tvp34SWN8IovijKFut6ZZPqUJRprpbNzLU7dezLL8LuKXVkCiwBUcbxe9gwt4ct7H/qJb9T0W7cmT9Suc99J6/JZxEl8jldRKMbLffhjAMc/gOL2Y46O6Z2XUJ997LKu1HMBJzXkuXwzfehmWNNpJmlRB+lUqS3QVlANDFNu8iXWvDOFII83ZAk/ddjHLGncRvXgykjgYBzx/D2jFB3d9iZ88c81HVr3MNxZ2sbnSAl+ffwPL3J8gziJkW9sNTChI1W9euZCM/xvRhGU7Xw1AThR9rrElPR84HbaMwLMDsDA/u9qt47mUssUQaFCONerRSJ75Df08edtFLMvuIXpxOSQOuAbP2wMIVz3zIx4fughxdrVs3+o8e+bCeefnlvqvPNb/WyzrfRKlmrtN2X8j/rRIzyTgpn4BbcddXTCXQrn4WDN+pcjS0r91JjT4MBGewAq9wyyklAvFGkxUDOLYECEey9CQH+fR269gWfMeoo1LwShwwfV3g/a5Ye2/8/jgReRyfTTlHEqVIP/w0wMPjW6meXt8Orh5iIMlaOXutx8C6KoYtotRiJFZjTkDInLICI51khyB/hKc1ga/eToMV18dCTF17zDU0Ddmf6EcSAppWvNDvPDe01nZuJXwpcVgHIwLntcHjvCmdffxkz1XkMvvw6mzz81NPkOF2uInH+p9tnfP6bmJ6ErQwzccUAZkVeGjxk2GjaOZ7ZgzIBln/8i54AmV46kSFLHM7i3L4bKFsLt4nEmswxhwv55H2TViiGOD8iAp+KSzFX7+rktY2tRH+MpC0A7GEXxvJ0jIm3c8yk+TS8k0DqB0jKmrHWMMzXmPoFo+6f4XufuJ4CYQdZ0c7Ho48u84LnMacwWkmuwf5Rgiw8TxVJNIvRgiTODj51rjvq9sdf0JAcO1YGwfMVQDEA/0mEtzwzDPvmcVZ7RuIdzYBYmLcQXf3wni8PYdP+XB4TeQbgXV2oDlMw9cec1pj+JI4Za/3HHK4+hFi1HBgRUsFVlDUUFJZj/mXOSgDikwKjjHqWaUwFDVpno/fh588lFL2WfdY/cijLE2I9awbcRQqYGTgmTYoSk3wnPvPYuljf0EL3VC7IMrpJxdYBQ3bvs5D42cTz6jkdgQ57OoSg1VLE2ReZOZTFSa/MTQFegySN6+ELuQqQ5Jw5ZXSJKZs3onwsvKTA9CbXywOdpfb8Dx2JPeIryxG377bPjKOujKHZuRnwQj0rBlyFCugZeCaMShvWmQp2670IKxsQO0h3Eh7e2AJMPVr/wHj42tojGjEWOItbXxOptFlUoHxHy2MMXjHfOeAW8ME7XY30YCLclDLM/UiNSsS0yPCZCUewgLsSeJ2JxoTj3eulFtYLACHzgDdozBD7dZqZmLlEx6U7GGrUOGUgB+CsIRh8bcOKvf80ZObt5J7aV2JPEwDqSd3WDS3LT5ER4bW0VL2ia7kvoyk0SjfR/j+0gQTJVilpMM2XQfVzWvgahh/41mIqToruGpRXNfpxfOlTqJDrUBYngW4dTjjhHqiazxAO64wFaRvDRki+20mQMYCWwa0hQDSKegNuIwr3GQ1e9+I8satlHd0IpoG/Sl3V7QLtdt+AWPjJ5PR9bYbWh6uiYwGNdB+ymcWm1qkqMkxxn5HZyc7oekoX4TLuJWQPWuRicgJ8aRnxGQyqFsL66wzoF3n4jgWolNZi1ogD+6yPCRh60X1paZGZTJIsR0XU1tHtKUapD2oTrqkMuWefz2q1jWuo3axhbEOBhXyDj9YFxueeUxHhk7n3nZeo3tTN/jqKnXBCDOsSqzG7wC1Lrs71WBvZXO+N62z+xN5uXQtdqcSmh/f66A+P5h3KSEnSbmhJW6OwJ9RTi1FT57CfyPx23QmHNn4LSmGfBNg5qJGmRSUC44NOTLrH7XJaxs3UB1cxNiBOMIGWcfALdteJAHhi+lM2s5G30047SfMQQVc23zMyARpp74IDPCvZtvcT+2721/dd47+Y1g3FJC8moB4upD8dCwNjrBuy6VwJ4JuLIHfu9c+MLTsCAPvjoQlOne1CuDmmINsikojji0NYzx7O0XsLhlC9WtDaAF4ygy7iBoeMf6J7lv6BK6chaM5Eh0kQGJ46mZrWkPxxvj7MxOSLI2jQsgLutlMawZeV9Hrrj6tFObvlYozmUD5Ly5xSFxeOCIQtAhO5Wp09En8NLGxiTvOx0+fJaVmmha7sUAac9G9xsHNBNVyPpQHHNoa5zgqV+/0oKxIwfGqpxMahiMzy0v/Qf3DV9CdxacqYKJmQkwFUU4YYipB0hhkuOk1D5WpPdCXM9nSAxhE5uDhZAPeOr5wlf3DgRvbM27oBLE0Ucdc7YhM7GwRnhRhKtOJCBSN/LDVfjEG2yJ0L2bYHnLfgOeJLBxwDBes5X5hWGHtnyRdbdfQE/LJiq7bKoV5ZD1RsHAO156lAeGLqQna6xrezRnQQkSRhDH9Q2BCURNXNO1BjezCyqL6/p8jPVjZ/Hk2Gk0NZSIy5qfr913/9suXnRye9A0XgmSY96SMaOE5DKHjnwWch73n0g2eLo9mQigEMCfXQrXLIGtBbsTN9Hw8j5DMYB8GgqjDl1No6y5/VJ6mjdR2ZPGGI0Rh2x6DMTlpnVruG/4EpbmDQoz6zyLJLEtxAZi44Bb5aamZ8BIXVkJuGXWlRcTha34EtCQ8xgs1Dqee6nwzx2pFK6AmcqyzTDmHKm7h6c/EofHjeZF0aw60bv4HbGFdPPz8HdXwW8/ZOuEw9AwHkAuBcMjDi3ZCqtvu5Ilreup7ElhTIIRn3y6CFrxa8//lB8Nv4HlOTO1SWY25I5ogwQhRuxWnZr2yXgFVqb66+rKTG3iWV9dBMaZYk9aMmle2DV0a8sSPnjdyR1fr40GaHUCJSSODx1RbKXYw9qRE07Y1out95asZPz9m0AHsKcfmrIwPKpozlZ56l3XsKR1PeV+H0ME4pJPlcGB2194kHsHruSUvK3vmjUhqgSJYySKpgi2JM5zcmYPJ2X6IKnbDyeA6jweG10Fbnn/ynYFpYQXnix8OY7TS9yVHQQLOohmGHOWkJI+gicifDMj/L7w6mxJdpWt913aDPe+C677Juzbqli0eIwn3nkVi1qep7w3hSEA8clnqqDhtjWP8t2Bqzi1waaEzVwNWZJY4zlZKZ5kub75l5Dqg9Jy+7TuKE8XLufZ0gqa3cI0L9DQlPMpDpYzX/7l1n984w0rbgqHY5IZlWV6jnGIMzMgDjyrEh7UhhtfreYjjsD2ApzdCV9/m+J37x/g/hsvZVH7Vip9OQxlKxnpEGLhtrU/47sDV7Eih60BOhY6OowsIEoxmYpfldk1LYMqQInnWQ6pLvzaIDjO1KvGQKYtzdj64beopPej5y3u+MposYoc1sLPEZDmo8QOFY97ahE3vlqZP7CE67YCXNYDz350nHkT2wl2g3FDDC4NKVvxftuzj/LdfVdyet5gjhBnHFk6NFILpnztWpJC/CHOzW2FuGF//GE81lRXQgNo7eMEwQHMsCuC5/o8sqfvb1rO4t8b5zt9pcrhvK6WudmQcjLzKMaQaO5yYAev8iVAsWaInVPY463GOA4qjmjIxBgt3P7Mk9w3eCVnNNjeI8ekQlVdXU26u0ActXFl83Oc1rAeovrkqTJBuJSflc4DF4J841SbIjMtgM3mXKpjce7F5yb+LElcwhCC4MAxZ6NuwiMP7K6sr7/qgNT3NQZVQzV1Ifva1pLxgRq8/7lH+d7eS1iRNygxx27PRCxTOZ370IprG9eBW8CY+j5/VeKVuJvdcTeYEnEmS5TJoZID+SRjDA0NPus3Ff7bnt7KzS35NCSCaDU15h4YzkIXieGLCB8FFvAaXF5siFJnQ/e9fOiHAd/cciUXdBvC5BjU1MGOSjDZbUDZ/ytYltqLrbOqbxZVRV6IlkGSIqVKoCHK5vCr5anq+ulelzGaDS+Pfu60TPcDmUCI9NHvcsZpV+boQwyRo/lfr0lTsUm7Ehn2ydt550W3ce58w9bCcXaQmBTBKJ6yH6UkSz7dy0UNGyBurKvOBEyWH5avAAOOGFSSkHi+lZKDJtsYaMyn2LFn4rzn+vs+HrSVGfHHGE2NM5oanzsgRffoY8KFCY+vJMK+1woUA4yXDdf3GO5+G/Q0cnyg1N1dEyf7ybOomcubnmdxfiNEzVPqqhAu45HquXY/yOSfa02QzaEd9xBQBCHlO7y0c9//2DM+5o8nVUaCMiNB+RgkxDn6cBwQh7IRPvFadqx0FWwasXHKD261rvGG4f0lS3M16CaMrA1RYpuSJXBKug+cMsaoKUC2xN0U4k5QFetzCYhOMI5DlMkehhIxZLMuo0PBgv5d5Q+nlEtS0+jAHAOXpWc38gk4iu+K8PhrCYqjbJwyPwffe5tw3RJh47Cl52cNyiSbHERMdpRJEHDggvyGOn9Vf6Oq8MvgNEggJfFBlIsmymTRnoscwsoKrqvY01f8E9FJrimtbFHHXAHJpGY/Gn1IZfgj/RoaE6lLyrY6AXnPO+B9ZwpbRm3l/uxUmI0/TDT5B4ZK1ERXfgs3tq6GsL3edSMC3cz9lSvqf3XgyhOt0cohSqUPMe4GQzrtUthXmrcv0u/yz+lCL2udOyCl0uzHeAmqZf7DiflzqRcMvFbC4ilbxVKN4V9ugj+4UNhZsI0MXJmFuko0JrFiZdO1WS5ueInm9C5I8vX3FemPlrE6OOMA+3Ggx6lJ/LTNo5gDS1ZEQByhd/PYR6J9Fcxo7RjIRZnbSBToNJ/TLqvRr1E712k2ZagMA2X4m6vhS28SRqvQVwL3CKVSokCHkTXok+16NJyc2QOqZlvDGgFVZHvcTS1pAqkdVtBEa7TrkvipA9VWnRZL5X3G+sbfUNo6fFE+jOcOiM7NbSQ5qKQgdnm7wOhr3ZbaUbZooncCPnEB3P1W2wBm66h9TWZw2UwUT6nAyLjgGq5uXAfG20+2q5CHa+cfxn4c9FkIcSq9vzPCNErcVYpqmLCzv/SxanQM+ZBFxzApgzFEEQ0JhIrX/nLqmccto/DOlbCkWfjNHxhe7oeuVvv6dEfIGNDTvIAgamFF44tc2/xLCNotfyURJC38rPaGOqpmRnMkRqMdF62cevTOVFGbweB7DoWRymW1SjgjUT7jvEVzHAAq4R06YqvRzD++jV3HGedp6wavmgc/ebfw1jOEvaNMtTa36kqhwxgdxsikBxC7nJ3fiEr1g653z5EaoW5lV9Jdny05AnNh0I6D9nxb43UQfo6rqFXiRZGbXD53oz7HsS/mijjk3xw15bwcf93pcYDiCGwetX28vv9r8LlrhLES7C3WVZiCJIgwia7T47ZO6/T0blARk20GcEb4RXgmfeEC22niqByMoF33ENd6EpCwFtO/p3TT3APDOQzXqtn/eTBTE2nzuoEyaez3la0X9plL4bvvEtoysHegrrqmRdZVnYJ0hRtan4Y4O9VgAEm4t3I1JOBLNIu4xmCU7PfaDgJMPEUwGiyesw0pztYoC0jMDa7mXEdN27xfVx1hYvAd4dXKLs7GrpRC2DQKt66AFa3Cxx6GJzZoCBOyrtTbgDdwUm4jq3KvQNxcr72KIGljbXDG7KvBjUErByMK0cmhD20MRmTBnCXEr81+eBG/cbjYYzITGiRmqq3h63FNdkt9YRAWNcHD7xF+70oD4zGVEW2L1hOH5al+fH8UdKqufSoUkna2JAtmDYgYg1Fqfzxy0EMrpYiiZO6NlEXNcljv8oqZZruejKMW1UF5vVCpB5E7x2DvhOFvr3P43n9vZslSn2pfBFW4oe2X4EyQGLduP0Z5JLiYsbANkbns6JOpypVDFrqvqFZmrv9UR8h1zHa0G+g4akJO76+ofz1BcZSt/3pl2HDTaQ6rP9nMzTd0gerlOuebkDRgkCn78VTtLNsYTZIT8v1ag+OoYwgMZz/0bMyDBcVQCfdPDK+zCtuwz1CL4P+8F+79ZBstC8+GwSHcYAARBTrHS/HSuelaEcRoRGvMYVZeFCaks07vq6aylGJIwcCsJkJZUIqB7d7jO68fKJPkZKFi2DtkOG9Zhv4rv8fmc75F5DbA+HPsrC3l0fCNs9+pZrCqKklsbuQgQEQgSGLSKr1xzoBU9exGyWBqwuMyi+OIjKl350lgZ8GeQZVxed08sKlFYmBk1CAh9K96D89d9TScfisPjl2F6XNAB7PcrWYwIjZKN/qQZ9L1PSk9C7Kr5+z2et4sF4WAG/MNYt43m5t26tsMSiFsLRgWNggdOQiSV6/NxmyfQ2JDQ0EI8608f9H/paMr5trnNI+sNcRlDQ0G35thFRswykHpBK9Wwxy0o0pEKIyHdLXn9t12c9dXj+ClHX5tJnMQfQ2M1ngiirl0sle7qa+IyYPBprdfHyrbnEVkrKHvbqQyPw9ak52+sWk69TC9zIaDXj+Ix5v63eSOq+nt3yfjJDPDewy2zq6GsKAJ2jz40RbDt56LePClAEZj8DRO1pDGIDpBkmTqizPjBbyK3e8tWlt7ApTGazgYLr984a09C/Lf/9JvLXiVAsM6KimXD3mGNYEhr5NDdZBMY2SDOtvtCzgeVGvyAa+Be2IxWyLDMl7vSyCFYWAMhgSuWipcu8zn2Us8Hn4l5O61NQb7QsrVyOZHMoqMB/niGF61gnEcG48YKJdjCqNV2lp8zj+367fb52W+PzxRY84S8vPC7O8/EchryIf8a3MD7/OVZV213l8rJdg96WM1uxK9+ja+HRPEiZbFZ3fS352HYs38JQ6fFnPowQavmYQc9O9kuW97TmjJ2v3wz/cm/HxTjed3BwwOVijsGkaPlfbfQJzgekJ7s8+Fq1r5tTcvueWp54YeGByp0NTocdfHT5qbhLi5OQRcLowWuHp4wryvKYKuBssZJcYeymKMtRnVyBpxtx4LbBmDjaO4y1r53XSKP6nF4Cv+qCryDceY+wys4D/BNZneGCwZ9hUh5wvXn+Zy05l5Bop5tu1tYGtvA31DARPFkCTWZFIOCzoynHl6c/mMhc7l5QrPPfB4VF8YMncJGRyevQ1xBHZXzeMjMVdoAyll7UNDClpTFoxI2wKEWgLDFdvHtxxbSck4hM1ZOSUx7Lp4vqE7D4ORoOCDfmK+lkxzPF8PCTn4vTJFnkKkBd+3m5m8+uYiXT+MIHJ40jfcUBmkPFqGbz64jTCMaWr0uevjS+cmIS+Nz8FDgfd5Hlf4js1jV2P46W5qJzWyZXkTp788isL2bUQbdldiskpoz9UZilqCP1rma47HjQ/vE65fBC15KFf4usBdxvBZEf4QyL7e0uIqO+mV2Eo8GIIYipVpjK6Q+CK/V82Yr7amBaWxnbhn44bP9ELjLEaTgSahKZ0yX5pMSXsKto9DxuWRk5rlS5FGjYcwUrUHv6Rc+XZbRv7JmXb4jasgUuaGfI2b9Rb44cPwyg7bJkMJCYbPGZgvIn9rYOx1oVzqOZag3vCgHFpVNpnbkrje+9mVh1Cy1Be+eixkxMxeVtsseBmBdJnPq5i2GGsfRmp202ZPXv4445KbSGySyK1v73aEJuXwu0HCRx2hYzKY1QZGYu688VQeaPIgSNvTFibqey/FUNTG3JHy5PNJwjujxHwS4Ux5lW2HU6dZqrG1h0FiVdakU6KxZbVJgzzuxdyhtVlr5NjLbmYEcYl/5LE8DQuEFUabT+j6jSfGSkdKyQ9aM6wHlh5sosoxHUvzcGGn/HUwreuopyHwzaqdDXxmuAP6BR7cBH1loTnFVGmREsrAN0BWechlIP9UT1oekjI9HkrFrc9MJYLRmvUOa/H+vHykrXR4Rv5vxpULaeKqWJm1cpzB7YwSMlQ+uuGQxHzVrQeRGRd2TNhSnFtX8Hkl0DtB+jDzI5GBFo+/yyo+GGpWuPW0bxZ4drf503VK/tXT7Ipi2DMG2UXQ3Qgj0fTj7UAZ8yRGnkTJJ4FVynArYt6vzQy78g8jAZN1ZFJfUIk+UBoiXW/KXN//qA00plirRP5noHnAMZRkWq7neCmgmY/NG5oRB1wDbo5bE58rJ9vqlWNbgtOUl6+9HLCufdLbOijkz7i2XmqXhlxa/iCqmR9PpnkNkHXxcw6fMlk+WgRGQrh7SLgiBad6trGFTF/OdgYCA2tcYU0k8imdmKUCqwSuFeHaxHAy00oUDPvVpK4fzVeLrQdos5xWFTlST0/7bHOEHwnywyQx65vT7NMaqtX6h55AIm5GQLqbZzZukYaRxHxmuuexZQwiQ9+CNHfEZXvoweEOFtMG0g5UHYjhQYT74oS3T54ArYCxmvlIS6fcf1YXDycRlGIYNnCGK7S40B8dOTcEbDeG7a5wv3EgSmgRTbcWaRHMwtCYReVI9cQR8zTGjzRKGwmMYQRjBjO+7BXYlPiMqcD0OSkGHWxHC80JPk10toB0zJBy8gV6S3whKnOmq21nnvEQ9hWh3ZMvqJhSQ8oa8pn4sARIGViYAZWRj2wumOsrMVmvvvxjBZlBc+dyTx6ue5aEGjZo6GiABWmYqM2JjCzUx1SuJ1FWFYljF45fZ32DaL/BTmS/7TpM57/XFpDCwGFshkCQ5rRCbD7tmv3HUe8chUxeHmpYwFdrEUjVFnSoGfIIibHxytJGaMswMB7IF14ZNV/w6h2IGjzYG3D+d3Zxh+fyxUnuLtJWPZ7VAhfNt4BMhMfmPU3qr8mAb7LxwuTkTwWcr3FeYEZAdh+sahRkNUiZL2gfpZSVgr0l65e3t/Lnge1JTGrSHTxCbjvW8GS/DcE9h79tSvOhKGGJqnsxngu+MX+qIrkLYXgydxHE8HSv3eJ4TbeQ1XZP/euZFn5NAJm38FB3cLzCzUnBvM0x1uWLta15ctLyz3GNp6s7LF3tZiBSR/bQHKxqKmvwIEy58tE4Nj+etNgCJAmNfgN/0dTJb+tplZkdBnbH8MgYvDFrD3QZi3j9ylpeC0BaCgfxVUAcmDsn6gXhnmNraI1h+Kx27jAGkrQFaVLvH2mCTN2DiWJrLB3hQU/JAyHm5kksHRfCivlQoV/uMsLT07u8GQMvRrAvA9d1Q0fa2rLXLfX4agOyc+LAiNwoPuk5rPKU9bSKoe1WvbhdvtDTxnhks5YMjFsX2D0ab6DBMRB3Qi1TP9WzxJ1OHzdrNa1XloEkMnc6jXJN7Bw44Y0CewN4YBSu6IQlWRvAJeZXV1hmPh1BTx0oQEbRpVPmznjakah7i5D2eZkcf7+maG2GF0FjvN9LOVrKFAW5ccgM2p/9iGeqRu6cUOZPJ49iEAWJcHW2yAeyo9xVMwfujuoWmIjg4Zfh4qWweDl4xvYA+C8FSNBtV2lkQBf5QiYijVhDPlyxnFVzk3w0qNhzc/VkBlAxpz3jXgKjiW0z4iiI0vx1HPABV7GAaVIyUTN/cck8+c68HNVqcqh9C2N73lgc2rNJIq++0/m/CiDniF3pYyGX7UnMB6I6XzVpyBtT8u0Ol19E2hqY+tb6OR3Iou0p2ZzeAU118DMupcEx+Yvnx80/eSlLbTgawhTzt6X481G4IzjMLItvVeZLW8FzhfN7DPPSMB7/FwFk06BVF65rvujWXVHfsad0lmPiCxfw+ba0pRw8ZW1KX9GiMutVKeBEEKVhbB4kEdQcKHfwFdkitzBhrsez70sJ7Bkzf9hr5G5PWDdTUzYRCGswvk24rAd6WgyjtboKk19hQJIGcCM+rBMupO5VVSIYKkFHq/xJIcfWoaguFk59Jc/RwxEbg7BpBAaLVvdrY1vUtgifTRTXJ9O8Kl+B5/D/NSpuOlItl6RtlvLJ3XBGKJzabgiNbZrj/KoC0pWmoRCZPzP1aNYRy+SKw8tZxRcrhWkFCAJ+bG3AXL3O2IW2CNSgPaHNqc904PNM5MuXHWM+7tUZASUQafOWkpH3OoZvHem7VJ3YfGoP9E4IF3cb2lKGQu2EtGh/7QEJy+ZLRjPPYA35WGD7tWd8+VQlwEzySLqeJcy4h1UJhzvPUWk5sIokdqCtA5r8/Qe91MuGPruzwntKNdp8tT+BExjzx8aRb80m2+N7sKkEQ3uEizuhJ2Oohb+CgJQi3jJ5tkdirO1YmJYHVnXyo+o0Q+krKESwp2xXtxyokg7Yb1o/2Cz2kgNP2Ek0tGZgsWuPbZ20Bb4wPhHKn08Y87+mx5kKVoI5H1gzm4dsS9v45Ce74G1LoCEN5eqvGCCO4lkDb/EcGChCoElkIX+4N2/dyalF6EI8DqmSZU4PiO4Vv2QaXa0N+IbtqeRApDIODI7DxmGrlqZ4KQ25FF/ONPDuAC5MyZSa3KtieWkuD9rqWCLyqV64eLF1UIJfJUC6G+U9vUXzg3LI5aMBdKfl3V6Jzf3jB5KGxrZGt7opOUQ/vSLIJ5Qyf58kkE/JPTmXP4oOOq9QC5CCYtN+WzF5jSTQLvK+Fs88NBFwkuNQVkY+qBLmvMYbFYzXGwzMb/zPCcj/A9mrY7/EcYAjAAAAAElFTkSuQmCC)
