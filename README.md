This is a personal reference guide for various setups, syntax, etc...

# Index
- [JS/Node Terminal Operation](#js/node-terminal-operation)
- [Pug (Jade)](#pug-(jade))
- [Sass](#sass)

# JS/Node Terminal Operation

Use javascript and node to run terminal commands.

[Source: Stack Overflow](https://stackoverflow.com/questions/20643470/execute-a-command-line-binary-with-node-js)


#### Node.js ^8.1.4
```javascript
const { exec } = require('child_process');
exec('touch index.html && mkdir assets', (err, stdout, stderr) => {
  if (err) {
    // node couldn't execute the command
    return;
  }

  // the *entire* stdout and stderr (buffered)
  console.log(`stdout: ${stdout}`);
  console.log(`stderr: ${stderr}`);
});
```

#### Using with Promises
```javascript
const util = require('util');
const exec = util.promisify(require('child_process').exec);

async function ls() {
  const { stdout, stderr } = await exec('ls');
  console.log('stdout:', stdout);
  console.log('stderr:', stderr);
}
ls();
```

#### Receive data in chunks (output as stream)
```javascript
const { spawn } = require('child_process');
const child = spawn('ls', ['-lh', '/usr']);

// use child.stdout.setEncoding('utf8'); if you want text chunks
child.stdout.on('data', (chunk) => {
  // data from standard output is here as buffers
});

// since these are streams, you can pipe them elsewhere
child.stderr.pipe(dest);

child.on('close', (code) => {
  console.log(`child process exited with code ${code}`);
});
```
#### Run
    node file.js

[Back to top](#index)

# Pug (Jade)

### Setup
    npm i pug-cli -g

### Watch and render changes
    pug -w ./input.pug -o ./output.html -P

Note: using `./` for input will watch for project-wide changes.

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

