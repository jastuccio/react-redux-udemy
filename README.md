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

import React from 'react';
import ReactDOM from 'react-dom';

// Create new component, should produce HTML
const App = function() {
  return <div>Hi!</div>div>;
}

// Take this component's generated HTML and put on the page (in the DOM)
ReactDOM.render(<App />, document.querySelector('.container'));
```
### Comments on above

- `const` ES6 syntax for declaring variable, not going to change as oppose to `var`
- `function() {}` can be replaced with `() => {}` **fat arrow** ES6 syntax
- **JSX** is a subset of JS which allows to write wht looks like HTML inside JS, but it is JS behind the scenes. 
- **JSX** has to be compiled to native JS
- `https://babeljs.io/repl/` a web tool to preview **ES6 compiled to native JS**

### ReactDOM vs React
- `import React from 'react` for imports core React library which works with components e.g. rendering, nesting (creating and managing components)
- `import ReactDOM from 'react-dom` for imports DOM React library which include functionality to take componenet and put it into DOM

## Class vs Instance of the component
- When creating component, we create **class component**
- Creating instance is i.e. `<App />` from class App `const App = function() {...`
- Render destination

















