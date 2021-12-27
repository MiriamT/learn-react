# Session 3: State Management in SPAs

## Objectives

- What is an SPA?
- Class Component state vs Functional Component hooks
- Code a simple counter component
- Assignment: Create a todo list

## What is an SPA?

A Single Page Application (SPA) is a web app that dynamically re-writes its content to respond to user interaction, instead of refreshing or loading a new page.

> Assignment: Read more about [SPAs](https://en.wikipedia.org/wiki/Single-page_application).

## Class Component state vs Functional Component hooks

React offers 2 ways to manage state:

1. a `state` object that exists in Class components (components that extend from `React.Component`)
2. state variables injected into Functional components via the `useState` hook

### Class Component State

A Class component manages an internal `state` object that is updated by calling its `setState()` function.

> Assignment: Read more about [Class components](https://reactjs.org/docs/state-and-lifecycle.html#converting-a-function-to-a-class)

```jsx
import React from "react";

class ClassComponent extends React.Component {
  // initialize the component's `state` variable
  state = {
    // initialize a `name` variable inside `state` with a default value of 'Miriam'
    name: "Miriam",
  };

  render() {
    return (
      <>
        {/* Render the current `name` value from `state` */}
        <div>My name is {this.state.name}</div>

        {/* Update the `name` value in `state` when the button is clicked
        by calling `this.setState()` with a new value */}
        <button onClick={() => this.setState({ name: "Teitelbaum" })}>
          Change Name
        </button>
      </>
    );
  }
}
```

[Live example](https://jscomplete.com/playground/s782493)

### Functional Component Hooks

A Functional component manages state as an internal variable provided by the `useState()` hook.

> Assignment: Read more about [Functional component hooks](https://reactjs.org/docs/hooks-intro.html)

```jsx
import React, { useState } from "react";

const FunctionalComponent = () => {
  // destructure a named variable and a setter function from the `useState` hook
  // the default value of the variable is passed as an arg to `useState`
  const [name, setName] = useState("Miriam");

  return (
    <>
      {/* Render the current `name` value from the variable */}
      <div>My name is {name}</div>

      {/* Update the `name` value in the variable when the button is clicked
      by calling the named setter function with a new value */}
      <button onClick={() => setName("Teitelbaum")}>Change Name</button>
    </>
  );
};
```

[Live example](https://jscomplete.com/playground/s782481)

## Code a simple counter component

To demonstrate the difference between Class Component state and Functional component hooks, we will code a simple Counter component using both methods of state management.

### Class Component Counter

```jsx
import React from "react";

class ClassCounter extends React.Component {
  constructor(props) {
    super(props);

    // bind the custom functions so that `this` is properly referenced when the
    // functions are passed down to the <button>
    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
  }

  state = {
    count: 0,
  };

  increment() {
    this.setState((prevState) => ({
      count: prevState.count + 1,
    }));
  }

  decrement() {
    this.setState((prevState) => ({
      count: prevState.count - 1,
    }));
  }

  render() {
    return (
      <>
        <div>Count: {this.state.count}</div>
        <button onClick={this.increment}>+</button>
        <button onClick={this.decrement}>-</button>
      </>
    );
  }
}
```

[Live example](https://jscomplete.com/playground/s782503)

### Functional Component Counter

```jsx
import React, { useState } from "react";

const FunctionalCounter = () => {
  const [count, setCount] = useState(0);

  function increment() {
    setCount(count + 1);
  }

  function decrement() {
    setCount(count - 1);
  }

  return (
    <>
      <div>Count: {count}</div>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </>
  );
};
```

[Live example](https://jscomplete.com/playground/s782519)

## Assignment: Create a Todo list

Create a new top-level component named `<Todo>` nested under the main `<App>`.

The `Todo` component should render a UI to enable users to:

1. Create a new Todo item with a custom `title` and `description`
2. Delete an existing Todo item
3. View all Todo items

Use components from the [Material UI library](https://mui.com/components/buttons/) to improve the user experience.

Feeling fancy? Add drag-and-drop functionality to allow users to sort their Todo items.
