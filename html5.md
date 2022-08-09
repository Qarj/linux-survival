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

create an anchor tag

```html
<a name="section-css">CSS Section</a>
```

jump to anchor tag (will work on initial page load also, no JavaScript required)

```html
<a href="#section-css">Jump to CSS section</a>
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
| `<nav>`     | Navigation, nav-bar        |

## Forms

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My web page</title>
        <style></style>
    </head>
    <body>
        <form>
            <div>
                <label for="name">Name</label>
                <input id="name" type="text" />
            </div>
            <div>
                <label for="email">Email</label>
                <input id="email" type="email" />
            </div>
            <button type="submit">Register</button>
            <button type="reset">Clear</button>
        </form>
    </body>
</html>
```

## Datalist

Use built in browser feature to provide a list of options for a user to select.

Every browser implements this feature differently.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <input type="text" list="countries" autocomplete="off" />
            <datalist id="countries">
                <option data-value="1">Australia</option>
                <option>Canada</option>
                <option>India</option>
                <option>United States</option>
            </datalist>
        </form>
    </body>
</html>
```

```css
form {
    width: 50%;
    padding: 2rem;
}

textarea {
    resize: none;
}
```

## Dropdowns

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <select>
                <optgroup label="Front-end Courses">
                    <option value="1">HTML</option>
                    <option value="2">CSS</option>
                    <option value="3">JavaScript</option>
                </optgroup>
                <optgroup label="Back-end Courses">
                    <option value="10">Node.js</option>
                    <option value="11">ASP.NET</option>
                    <option value="12">Django</option>
                </optgroup>
            </select>
        </form>
    </body>
</html>
```

Can apply attributes like

-   `multiple` to allow multiple selections (to select element)
-   `selected` to select an option by default
-   `disabled` to disable an option (will not be selectable)

## Checkboxes

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <div>
                <input type="checkbox" id="front-end" />
                <label class="label-inline" for="front-end">Front-end</label>
            </div>
            <div>
                <input type="checkbox" id="back-end" checked />
                <label class="label-inline" for="back-end">Back-end</label>
            </div>
        </form>
    </body>
</html>
```

## Radio Buttons

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <div>
                <input type="radio" name="membership" id="silver" checked />
                <label class="label-inline" for="silver">Silver</label>
            </div>
            <div>
                <input type="radio" name="membership" id="gold" />
                <label class="label-inline" for="gold">Gold</label>
            </div>
        </form>
    </body>
</html>
```

## Sliders

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <input type="range" min="0" max="100" value="70" />
        </form>
    </body>
</html>
```

## File Uploads

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <input type="file" accept=".jpg" />
        </form>
    </body>
</html>
```

## Grouping Related Fields

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <fieldset>
                <legend>Billing Address</legend>
                <input type="text" /><input type="text" /><input type="text" />
            </fieldset>
            <fieldset>
                <legend>Payment</legend>
                <input type="text" /><input type="text" /><input type="text" />
            </fieldset>
        </form>
    </body>
</html>
```

## Hidden Fields

For sending required info back to the server.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <input type="hidden" name="course-id" value="1234" />
        </form>
    </body>
</html>
```

## Form Validation

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form>
            <input type="text" required minlength="3" maxlength="10" />
            <input type="email" />
            <input type="date" />
            <input type="password" />
            <input type="number" min="-5" max="15" />
            <button type="submit">Submit</button>
        </form>
    </body>
</html>
```

## Form Submission using Formspree

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My form</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
        <!-- Milligram CSS -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css" />
    </head>
    <body>
        <form action="https://formspree.io/f/mjvzvkbv" method="POST">
            <input type="text" placeholder="Name" name="name" />
            <input type="text" placeholder="Email" name="email" />
            <button type="submit">Submit</button>
        </form>
    </body>
</html>
```

## Full example form from exercise solution

https://codewithmosh.com

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Login</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>
    <body>
        <form class="form-signin" action="" method="POST">
            <h1>Please sign in</h1>
            <div class="form-group">
                <input
                    class="form-control"
                    type="text"
                    placeholder="Email address"
                    minlength="5"
                    maxlength="255"
                    autofocus
                />
            </div>
            <div class="form-group">
                <input class="form-control" type="password" placeholder="Password" maxlength="255" />
            </div>
            <div class="form-group">
                <input type="checkbox" id="remember-me" />
                <label for="remember-me">Remember me</label>
            </div>
            <button class="btn">Sign in</button>
            <p class="muted">Copyright &copy; 2020</p>
        </form>
    </body>
</html>
```

```css
html {
    font-size: 62.5%;
}

body {
    align-items: center;
    background: #f5f5f5;
    display: flex;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans',
        'Helvetica Neue', sans-serif;
    font-size: 1.6rem;
    height: 100vh;
    justify-content: center;
}

.form-signin {
    max-width: 300px;
    text-align: center;
    width: 100%;
}

.form-control {
    border: 1px solid #ced4da;
    outline: 0;
    transition: border 0.15s, box-shadow 0.15s;
}

.form-control:focus {
    border: 1px solid #86b7fe;
    box-shadow: 0 0 0 5px #b9d3fa;
}

/* One place to define the common properties for buttons and input fields.  */

.form-control,
.btn {
    border-radius: 5px;
    /* The default box-sizing for input fields is content-box. So, any padding we apply to an input 
  field, increases its width. To ensure that input fields and buttons have the same width, we need
  to set box-sizing to border-box. */
    box-sizing: border-box;
    padding: 1.5rem;
    /* It's a common technique to set the width of input fields and buttons to 100% so they fill up
  their container. We can then control their size through their container (in this case form-signin) */
    width: 100%;
}

.btn {
    background: #0d6efd;
    border: 0;
    border-radius: 30px;
    color: #fff;
    cursor: pointer;
    outline: 0;
}

.btn:hover {
    background: #0759d3;
}

/* We use this class to add vertical space between different input fields. */

.form-group {
    margin: 1rem 0;
}

/* A reusable class. */

.muted {
    color: #6c757d;
}
```
