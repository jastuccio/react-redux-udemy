# React Redux notes

## Boiler plate

React Components in ES6
Tooling (to transpile JSX + ES6 to ES5)
Webpack and Babel will do the tranpile, compilation
(Webpack+Babel compile JS files to bundle.js - see `<script>` tag in index.html)

## Scaffolding project

- Get repo `git clone https://github.com/StephenGrider/ReduxSimpleStarter.git`
- Change to folder `ReduxSimpleStarter`
- Install dependancies `npm install`
- Run project `npm start`
- Visit `localhost:8080`

## Default component 

```javascript
import React from 'react';
import { Component } from 'react';

export default class App extends Component {
  render() {
    return (
      <div>React simple starter</div>
    )
  }
}
```

## What is component

- React JS library is used to produce HTML that is shown to the user in the web browser. 
- When writting React code we write inidividual **components** or **views**
- Snippets of code in JS which produce HTML 

```javascript

// Create new component, should produce HTML
const App = function() {
  return <div>Hi!</div>div>;
}

// Take this component's generated HTML and put on the page (in the DOM)

```
### Comments on above

- `const` ES6 syntax for declaring variable, not going to change as oppose to `var`
- `function() {}` can be replaced with `() => {}` fat arrow ES6 syntax
- **JSX** is a subset of JS which allows to write wht looks like HTML inside JS, but it is JS behind the scenes. 
























