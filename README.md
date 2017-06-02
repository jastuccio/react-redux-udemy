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

`
import React from 'react';
import { Component } from 'react';

export default class App extends Component {
  render() {
    return (
      <div>React simple starter</div>
    )
  }
}

`