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
