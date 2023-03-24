---
title: "Pug"
date: 2022-09-13T21:08:49+05:30
draft: false
---

Pug is HTML templating engine. Pug compiler convert pug code into HTML code, that browser can understand.

Pug has powerful features like conditions, loops, includes, mixins using which we can render HTML code based on user input or reference data. Pug also support JavaScript natively, hence using JavaScript expressions, we can format HTML code.

### Installation

Pug can be installed using npm.

```bash
npm install pug
```

### Overview

The rendering process of Pug is pretty straightforward. Pug compiler will compile Pug source code into Javascript function that function will take object as argument. Pug will call that function with provided data and return a string of HTML rendered with your data.

template.pug
```pug
  p `Hello #{name}`
```

index.js 
```js
  // Require pug library
  const pug = require('pug');

  // Compile the source code
  const compiledFunction = pug.compileFile('template.pug');

  // Render a set of data
  console.log(compiledFunction({
    name: 'World'
  }));
  // "<p>Hello World</p>"
```

renderFile() method combines compiling and rendering is as follows :  


index.js
```js
 // Require pug library
  const pug = require('pug');

  // Compile template.pug, and render a set of data
  console.log(pug.renderFile('template.pug', {
    name: 'World'
  }));
  // "<p>Hello World</p>"
```