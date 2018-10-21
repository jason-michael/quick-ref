This is a personal reference guide for various setups, syntax, etc...

# Index
- [Pug (Jade)](#pug-(jade))
- [Sass](#sass)

# Pug (Jade)

### Setup
    npm i pug-cli -g

### Watch and render changes
    pug -w ./jade -o ./html -P

| Flag      | Description                           |
| ---       | ---                                   |
| `-w`      | watch file                            |
| `./jade`  | where to watch for changes            |
| `-o`      | output                                |
| `./html`  | where to render the output            |
| `-P`      | pretty print (not minified, optional) |

### Syntax

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

# Sass

### Setup
    npm i sass -g

### Build
    sass source/path/main.sass build/path/main.css

### Watch for changes and compile
    sass -w path/file.sass:path/file.css

### Syntax
```
// _reset.sass

html,
body,
ul,
ol
  margin:  0
  padding: 0
```
```
// _base.sass

@import reset

$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color

nav
  ul
    margin: 0
    padding: 0
    list-style: none

  li
    display: inline-block

  a
    display: block
    padding: 6px 12px
    text-decoration: none
```

## Sass folder structure examples

### Simple structure
- modules/
  - _color.sass
  - _typography.sass
- partials/
  - _base.sass
  - _navigation.sass
- vendor/
  - _bootstrap.sass
- main.sass

#### Use

- **modules**: Code to include but not compile.
- **partials**: Code to include and compile.
- **vendor**: 3rd party code.
- **main.sass**: uses `@import` to include all the other files. 



### 7-1 pattern
- base/
  - _reset.sass
  - _typography.sass
  - _color.sass
- components/
  - _buttons.sass
  - _navigation.sass
  - _gallery.sass
- layout/
  - _header.sass
  - _grid.sass
  - _sidebar.sass
- pages/
  - _home.sass
  - _about.sass
  - _contact.sass
- themes/
  - _theme.sass
  - _admin.sass
- helpers/ (or utils/)
  - _variables.sass
  - _functions.sass
  - _mixins.sass
- vendors/
  - _bootstrap.sass
  - _jquery-ui.sass
- main.sass

#### Use

- **base**: boilerplate content, site-wide styles.
- **components**: micro layout (buttons, navigation, etc..).
- **layouts**: macro layout, major sections (header, footer, grid system, etc..).
- **pages**: page specific styles.
- **themes**: project specific themes, e.g. different color schemes in different sections.
- **helpers**: Sass tools, helper files, variables, config. These will not be compiled.
- **vendors**: 3rd party code.
- **main.sass**: uses `@import` to include all the other files. 

[More on directory structure](https://vanseodesign.com/css/sass-directory-structures/)

[Back to top](#index)

