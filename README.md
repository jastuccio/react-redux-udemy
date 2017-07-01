# React notes

## Boiler plate

React Components in ES6
Tooling (to transpile JSX + ES6 to ES5)
Webpack and Babel will transpile, compile
(Webpack+Babel compile JS files to bundle.js - see `<script>` tag in index.html)

## Scaffolding project

- Get repo `git clone https://github.com/StephenGrider/ReduxSimpleStarter.git`
- Change to folder `ReduxSimpleStarter`
- Install dependencies `npm install`
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
// function() is replaced with ES6 fat arrow () => {}
const App = () => {
  return <div>Hi!</div>div>;
}

// Take this component's generated HTML and put on the page (in the DOM)
ReactDOM.render(<App />, document.querySelector('.container'));
```

### Comments on the above

- `const` ES6 syntax for declaring variable, not going to change as oppose to `var`
- `function() {}` can be replaced with `() => {}` **fat arrow** ES6 syntax
- **JSX** is a subset of JS which allows to write what looks like HTML inside JS, but it is JS behind the scenes 
- **JSX** has to be compiled to native JS
- `https://babeljs.io/repl/` a web tool to preview **ES6 compiled to native JS**

### ReactDOM vs React
- `import React from 'react` for imports of core React library which work with components e.g. rendering, nesting (creating and managing components)
- `import ReactDOM from 'react-dom` for imports of DOM React library which include functionality to take componenet and put it into DOM

## Class vs Instance of the component
- When creating component, we create **class component**
- Creating instance is i.e. `<App />` from class App `const App = function() {...`
- Render destination by targeting DOM element i.e. element HTML class `document.querySelector('.container')`

## Exporting modules, classes and setting/changing state

### EXPORTING
```javascript

import React from 'react';

const SearchBar = () => {
  return <input />
}

// exporting only SearchBar component
export default SearchBar;

```

### IMPORTING
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import SearchBar from './components/search_bar';

const App = () => {
  return ( 
    <div>
      <SearchBar />
    </div>
  )
}

ReactDOM.render(<App />, document.querySelector('.container'));

```


## Exporting modules
- `export default SearchBar` makes sure that component is enabled to `import` statement in other files, imports SearchBar const only
- `import SearchBar from './components/search_bar'` put into the file which is using `<SearchBar />` makes sure that it will be available there, no need to use search_bar.js it assumes that it is JS file as a default, make sure that the relative path is correct.

## Class vs Functional components

- Class component when we want that to be aware of itself via state vs dummy functional to e.g. only render to the screen

### FUNCTIONAL
```javascript
import React from 'react';

const SearchBar = () => {
  return <input />
}

// exporting only SearchBar component
export default SearchBar;

```

### CLASS
```javascript
// import React from 'react';
   import React, { Component } from 'react';

// class SearchBar extends React.Component {
   class SearchBar extends Component {
    render() {
      return <input />;
    }
  }

export default SearchBar;

```

- Creates new class SearchBar and gives it access to all functionalities React.Components has
- render() method has to return() JSX otherwise there will be an error

## Event handler

```javascript
import React, { Component } from 'react';

class SearchBar extends Component {
  render() {
    // alternatively return <input onInputChange={event => console.log(event.target.value)} />;
    return <input onChange={this.onInputChange} />;
  }

  // event handler
  onInputChange(event) {
    console.log(event.target.value);
  }
}

export default SearchBar;

```

## State

- State definition is plain JS object that is used to record and react to user event
- Each class based component has it own state object
- Whenever component's state is changed, component immediately rerenders and forces all its children to rerender as well
- `constructor(props)... super(props)... this.state=` initialize state in a class based component
- constructor function is reserved to do set up inside the class
- super for calling method on parent class

```javascript
import React, { Component } from 'react';

class SearchBar extends Component {
  constructor(props) {
    super(props);

    this.state = { term: '' };
  }

  render() {
    //return <input onInputChange={event => console.log(event.target.value)} />;
    // changed to
    //return <input onChange={event => this.setState({ term: event.target.value })} />;
    // and now to...
    return (
      <div>
        <input onChange={event => this.setState({ term: event.target.value })}>
        Value of the input: {this.state.term}
      </div>;
    )
  }
}

export default SearchBar;

```

## Updating state
- Only inside the constructor function we manipulate the state `this.state = {};`
- Outside constructor change should be done with `this.setState = {};`
- State should tell input what the current value should be therefore above example needs to be refactored - controlled components
-  **controlled component** has its `value` set by state - see second example below (value changes when state changes)

```javascript
render() {
    return (
      <div>
        <input onChange={event => this.setState({ term: event.target.value })}>
        Value of the input: {this.state.term}
      </div>;
    )
  }

```

### Change to the below for **controlled component**


```javascript
render() {
    return (
      <div>
        <input 
          value={this.state.term}
          onChange={event => this.setState({ term: event.target.value })};
        />    
      </div>;
    )
  }

```

## Downwards data flow
- Only the most parent component in application should be responsible for fetching data

## Code simplification - ES6 syntactic sugar example
Whenever we have key/value of exact the same string it can be simplified with ES6 syntax
e.g. `this.setState({ videos: videos });` to `this.setState({ videos });`


### Notes
- when refactorfing functional to class based component make sure you reference to `this.props` as oppose to just `props` as an argument in functional component

```javascript
import React from 'react';

//Functional component (props) is the argument being passed
const VideoList = (props) => {
  return (
    <ul className="col-md-4 list-group">
      {props.videos.length}
    </ul>
  );
};

export default VideoList;

```

# Redux notes

- Predictable state container for JavaScript applications
- Redux is data contained in application box, React is views contained in application box
- State Container a collection of all data that describes the app
- Redux centralise all the application data inside a single object

## Reducers

- Reducer is a function that returns a piece of application state
- Reducers produce value of the state

```javascript
// Application State generated by reducers
{
// Books reducer
books: [ {title: 'Harry Potter'}, { title: 'King of the Jungle'}],
// ActiveBook reducer
activeBook: {title: 'HarryPotter'}
}
```
- **Container** is a React component that has a direct connection to the state managed by Redux
- Component where state is injected to will be promoted to container = so called 'smart components'

## mapStateToProps

- mapStateToProps takes the application state and whatever is returned from that function is what is going to show up as props inside the container above e.g. 'class BookList extends...'

```javascript
import React, { Component } from 'react';
import { connect } from 'react-redux';

class BookList extends Component {
  renderList() {
    return this.props.books.map((book) => {
      return (
        <li key={book.title} className="list-group-item">{book.title}</li>
      );  
    });
  }

  render() {
    return (
      <ul className="list-group col-sm4">
        {this.renderList()}
      </ul>
    )
  }
}

function mapStateToProps(state) {
  // whatever is returned will show up as props
  // inside of BookList
  return {
    books: state.books // returns an object with key books available for this.props.books equal to state.books - coming from Redux, a glue between React here and Redux object
  };
}

// connect takes a function and a component and produces a container
export default connect(mapStateToProps)(BookList);
```

## Action and Action Creators
- action creator returns an object
- returned object is automatically send to all different reducers - will flow through all reducers in an app
- reducers can choose depending on the action to return different pieces of state depending on what the action is

### Process illustration
// click => action creator => action => active book reducer => object returned contains same/new activeBook property => app components rerender

```javascript
// action creator
function( return {
  type: BOOK_SELECTED
  book: { title: 'Book2'}
})

// action
{
  type: BOOK_SELECTED
  book: { title: 'Book2'}
}

// active book reducer
switch (action.type) {
  case BOOK_SELECTED:
    return action.book
  default:
  // I dont care about this action do nothing return currentState
}

// activeBook property returned from book reducer
{
  activeBook: {title: 'JavaScript'}
  books: [ {title: 'Dark Tower'}, {title: 'JavaScript'}]
}
```

```javascript
// newly updated book-list.js

import React, { Component } from 'react';
import { connect } from 'react-redux';
import { selectBook } from '../actions/index';
import { bindActionCreators } from 'redux';


class BookList extends Component {
  renderList() {
    return this.props.books.map((book) => {
      return (
        <li key={book.title} className="list-group-item">{book.title}</li>
      );  
    });
  }

  render() {
    return (
      <ul className="list-group col-sm4">
        {this.renderList()}
      </ul>
    )
  }
}

function mapStateToProps(state) {
  // whatever is returned will show up as props
  // inside of BookList
  return {
    books: state.books
  };
}

// Anything returned from this function will end up as props
// on the BookList container
function mapDispatchToProps(dispatch) {
  // Whenever selectBook is called, the result should be passed
  // to all of our reducers
  return bindActionCreators({ selectBook: selectBook }, dispatch);
}

// Promote BookList from a component to a container - it needs to know
// about this new dispatch method, selectBook. Maker it available
// as a prop.
export default connect(mapStateToProps, mapDispatchToProps)(BookList);

```

