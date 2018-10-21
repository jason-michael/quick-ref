This is a personal reference guide for various setups, syntax, etc...

# Index
- [Pug (Jade)](#pug-(jade))

# Pug (Jade)

## Setup

    npm i pug-cli -g

## Watch and render changes

    pug -w ./jade -o ./html -P


| Flag      | Description                           |
| ---       | ---                                   |
| `-w`      | watch file                            |
| `./jade`  | where to watch for changes            |
| `-o`      | output                                |
| `./html`  | where to render the output            |
| `-P`      | pretty print (not minified, optional) |

## Syntax

```pug
doctype html
html(lang="en")
  head
    title Document
    meta(charset="UTF-8")
    meta(name="viewport", content="width=device-width, initial-scale=1.0")
    meta(http-equiv="X-UA-Compatible", content="ie=edge")
    link(rel="stylesheet", href="assets/css/style.css")

  body
    main.container
      .header
        ul.nav
          li: a.nav-link.current(href="#") Home
          li: a.nav-link About
          li: a.nav-link Contact
    section#hero
    section.section.section-2

    // New line html comment
    <!-- inline html comment -->    

    script(src="assets/js/main.js")

```
[Back to top](#index)
