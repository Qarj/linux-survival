# html 5

## Basic layout

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My web page</title>
        <style>
            img {
                width: 200px;
                border-radius: 100px;
                float: left;
                margin-right: 20px;
            }

            p.username {
                font-weight: bold;
            }
        </style>
    </head>
    <body>
        <img src="./images/Person.png" alt="The Person" />
        <p class="username">@username</p>
        <p>My text caption!</p>
    </body>
</html>
```

## img tag

does not require a closing tag in html5, but Prettier will put it there anyway

```txt
<img src="" alt="">
```

```html
<img src="" alt="" />
```

## validate html code

https://validator.w3.org/

## validate css code

https://jigsaw.w3.org/css-validator/

## Emet shortcut

In new `index.html` type `!` and press tab for generated template

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <body></body>
</html>
```

## Meta elements SEO

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta name="content" content="HTML, CSS" />
        <meta name="description" content="A very coool website using HTML and CSS" />
        <title>Document</title>
    </head>
    <body></body>
</html>
```

## Headings

6 headings H1 thru H6, should only be used for structure to create a hierarchy.

Should only be 1 H1. Should not skip levels.

```html
<body>
    <h1>Heading 1</h1>
    <h2>HTML</h2>
    <p>HTML tutorial</p>
    <h3>Code</h3>
    <h3>Exercise</h3>
    <h2>CSS</h2>
    <p>CSS tutorial</p>
    <p>It is fun to learn <em>HTML</em>!</p>
</body>
```

## HTML Entities

https://dev.w3.org/html5/html-author/charref

```html
<p>It is fun to learn &lt;HTML&gt;! &copy;</p>
```

`&nbsp;` is a non-breaking space
`&amp;` is an ampersand

## Lorem Ipsum

type `lorem` followed by number of words you want, say 10 and press tab.

10 words are generated

## Links

text link

```html
<a href="company/about.html">About me</a>
```

image link

```html
<img src="./images/Person.png" alt="Person" />
```

downloads image instead of displaying it

```html
<a href="./images/Photo.png" download>My Photo </a>
```

jump to anchor tag

```html
<a href="#section-css">CSS</a>
```

jump to top

```html
<a href="#">Jump to top</a>
```

open in new tab

```html
<a href="https://www.google.com" target="_blank">Google</a>
```

mail to link

```html
<a href="mailto:example@gmail.com">Email someone</a>
```

## unsplash.com - freely usable images

`object-fit: cover` will crop the image so it fills the container

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Document</title>
        <style>
            img {
                width: 200px;
                height: 200px;
                object-fit: cover
            }
        </style>
    </head>
    <body>
        <img src="./images/coffee.jpg" alt="A coffee mug on a table"></img>
    </body>
</html>
```

## sketch.com

https://www.sketch.com/

## pexels.com

Free stock photos and videos

https://www.pexels.com/

## caniuse.com

www.caniuse.com

## video and audio tags

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Document</title>
        <style>
            video {
                width: 400px;
            }
        </style>
    </head>
    <body>
        <p>What gives?</p>
        <video src="./videos/waves.mp4" controls autoplay loop>Your browser doesn't support videos.</video>
    </body>
</html>
```

`audio` tag works like the `video` tag

## Unordered list

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Unordered List</title>
        <style>
            ul {
                list-style-type: square;
            }
        </style>
    </head>
    <body>
        <ul>
            <li>About me</li>
            <li>
                Courses
                <ul>
                    <li>HTML</li>
                    <li>CSS</li>
                    <li>JavaScript</li>
                </ul>
            </li>
            <li>Subscribe</li>
            <li>Contact me</li>
        </ul>
    </body>
</html>
```

## Ordered list

vscode shortcut `ol>li*3`

```html
<ol>
    <li>Preheat the oven</li>
    <li>Place the ingredients on the crust</li>
    <li>Put the pizza in the oven for 22 mins</li>
</ol>
```

## Description list

```html
<dl>
    <dt>Title</dt>
    <dd>The Ultimate HTML and CSS Course</dd>
    <dt>Author</dt>
    <dd>Mosh Hamedani</dd>
    <dt>Skills</dt>
    <dd>HTML</dd>
    <dd>CSS</dd>
    <dd>Responsive Design</dd>
    <dd>Search Engine Optimisation</dd>
</dl>
```

will render like

```txt
Title
    The Ultimate HTML and CSS Course
Author
    Mosh Hamedani
Skills
    HTML
    CSS
    Responsive Design
    Search Engine Optimisation
```

## Semantic table with header and footer

better for screen readers

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Semantic Table</title>
        <style>
            table,
            td,
            th {
                border: 1px solid grey;
                border-collapse: collapse;
                padding: 5px;
            }
            tfoot {
                text-align: left;
            }
        </style>
    </head>
    <body>
        <table>
            <thead>
                <tr>
                    <th colspan="2">Expenses</th>
                </tr>
                <tr>
                    <th>Category</th>
                    <th>Cost</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Marketing</td>
                    <td>$100</td>
                </tr>
                <tr>
                    <td>Accounting</td>
                    <td>$200</td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <th>Total</th>
                    <th>$300</th>
                </tr>
            </tfoot>
        </table>
    </body>
</html>
```

# Div - generic container

`div` is a block level element. They always start on a new line. They take the full width of the container.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <style>
            div.product {
                background-color: gold;
                width: 300px;
            }
        </style>
    </head>
    <body>
        <div class="product">
            <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit.</p>
            <a href="../index.html">Home page</a>
        </div>
        <div class="product">
            <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit.</p>
            <a href="../index.html">Home page</a>
        </div>
    </body>
</html>
```

# Span - generic container

`span` is an inline element, it will not take the entire width of the container.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <style>
            .highlight {
                background-color: yellow;
            }
        </style>
    </head>
    <body>
        <p>
            <span class="highlight">Lorem</span> ipsum dolor sit amet consectetur adipisicing elit. Aliquid, laboriosam.
        </p>
    </body>
</html>
```

## Semantic elements

Helps search engines and screen readers. Also enables browser features.

examples

| semantic element | about                                                   |
| ---------------- | ------------------------------------------------------- |
| `<article>`      | Self contained piece of content                         |
| `<figure>`       | Image or diagram, can provide `<figcaption>`            |
| `<mark>`         | Highlighted text - yellow by default                    |
| `<time>`         | Date and time - can include machine readable `datetime` |

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>HTML</title>
        <style></style>
    </head>
    <body>
        <article class="article">
            <h1>Article title</h1>
            <p>Published <time datetime="2021-01-01 17:15">January 1 2021 05:15pm</time></p>
            <p>
                <mark>Lorem</mark> ipsum dolor sit amet consectetur adipisicing elit. Et, eum nisi, quia magnam dolor
                unde officia, modi dolore sunt cum totam placeat error corrupti repellat doloremque amet labore itaque
                architecto. Ratione ipsum atque hic quaerat harum eos optio dicta eveniet ducimus reiciendis cumque,
                quisquam numquam aut! Eius impedit nisi quod animi aspernatur ut recusandae facilis, quisquam a! A, ipsa
                ab. Odio aliquam rem fugit enim laborum sit labore commodi dicta perferendis nam a natus modi sequi, ex
                vitae officia sunt corrupti quis eius nesciunt quia earum voluptas deserunt. Dolorem, animi.
            </p>
            <figure>
                <img src="./images/Photo.png" alt="Some photo" />
                <figcaption>Me getting ready for battle.</figcaption>
            </figure>
        </article>
    </body>
</html>
```

## Structure a Web Page

| element     | about                      |
| ----------- | -------------------------- |
| `<main>`    | Main content, one per page |
| `<section>` | Sub content                |
| `<header>`  | Page header                |
| `<footer>`  | Page footer                |
| `<aside>`   | Sidebar                    |
| `<nav>`     | Navigation                 |
