# Session 5: Global State with React Context

## Objectives

- Avoid prop drilling with `useContext`
- Manage state changes with `useReducer`
- Assignment: Move the todo items to global state with a reducer

## Avoid prop drilling with `useContext`

Passing props from parent to child is the simplest way to share state across an application. When two components need to use the same data, that state is moved to a common parent of the components, and then passed down to the children. When many parts of an app require the state, it becomes "global" state since the entire app needs it. Using the logic of storing state in a common parent, global state ends up at the root component and then must be passed down through all the children so that the ones at the bottom can use it. This annoying practice is called "prop" drilling.

```jsx
<App>
  <AppChild>
    <AppGrandchild>
      <VeryNestedChild>
        {/* props must be passed from App -> AppChild -> AppGrandchild -> VeryNestedChild */}
      </VeryNestedChild>
    </AppGrandchild>
  </AppChild>
  <AppChild>
    <AppGrandchild>
      <VeryNestedChild></VeryNestedChild>
    </AppGrandchild>
  </AppChild>
</App>
```

React Context avoids prop drilling because the provided context state can be accessed by any child. For example, global state can be stored in `<App>` or some higher level parent component and a `<VeryNestedChild>` can subscribe directly to the context value instead of needing all its parents to pass down the state.

> **Assignment:** Read more about [React Context](https://reactjs.org/docs/context.html).

Here is an example of creating a theme, based off of the React example code for context:

```jsx
import React, { useState, useContext } from "react";

const themes = {
  light: {
    foreground: "#000000",
    background: "#ffffff",
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222",
  },
};

const ThemeContext = React.createContext();

function App() {
  const [theme, setTheme] = useState(themes.light); // default theme is light

  // create a function that can toggle themes
  const toggleTheme = () => {
    theme === themes.light ? setTheme(themes.dark) : setTheme(themes.light);
  };

  return (
    <ThemeContext.Provider
      // context value has the theme and also the toggle function
      value={{
        theme,
        toggleTheme,
      }}
    >
      <Toolbar />
      <Content />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function Content() {
  const { theme } = useContext(ThemeContext);
  return (
    <div
      style={{
        background: theme.background, // use the theme colors!
        color: theme.foreground,
        height: "10rem",
      }}
    >
      I am styled by theme context!
    </div>
  );
}

function ThemedButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  return (
    <button
      style={{
        background: theme.background,
        color: theme.foreground,
        marginBottom: "1rem",
      }}
      onClick={
        toggleTheme /* toggle function can be called by children to change the context state! */
      }
    >
      Change Theme
    </button>
  );
}

ReactDOM.render(<App />, mountNode);
```

[Live example](https://jscomplete.com/playground/s789760)

## Manage state changes with `useReducer`

[Redux](https://redux.js.org/) is a state management library that is very popular with the React community. So popular in fact that the React developers released a simpler version of it as a native React hook called `useReducer`.

The general idea of reducers is to simplify app logic by limiting the way that state can be changed. Instead of letting any code directly update state, changes are triggered through predefined `actions`. When an action is triggered, a `reducer` processes it and updates the state. Since only reducers can update state, and reducers only process actions, state update logic is separated from the rest of app logic. The app can still read the state, but if updates are required based on user interaction the app will trigger an action and let the reducer handle the rest.

> **Assignment:** Read more about [`useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer). You can also check out [A Cartoon Intro to Redux](https://code-cartoons.com/articles/a-cartoon-intro-to-redux/)

Let's demonstrate a basic reducer by re-writing our counter to use the `useReducer` hook instead of the `useState` hook.

As a reminder, here is the `useState` version:

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

To convert it to `useReducer` we need to identify the state, and the actions that change the state. Here the state would still be `count`, the same as it is above. And we have 2 natural actions, `INCREMENT` and `DECREMENT` that change the state. The `increment()` and `decrement()` functions become logic in the reducer. Try adding a `RESET` button in the example below to test out adding new actions.

```jsx
import React, { useReducer } from "react";

function countReducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      throw new Error(`Count Reducer does not recognize ${action.type}`);
  }
}

const ReducerCounter = () => {
  const [countState, countDispatch] = useReducer(countReducer, {
    count: 0,
  });

  return (
    <>
      <div>Count: {countState.count}</div>
      <button onClick={() => countDispatch({ type: "INCREMENT" })}>+</button>
      <button onClick={() => countDispatch({ type: "DECREMENT" })}>-</button>
    </>
  );
};

ReactDOM.render(<ReducerCounter />, mountNode);
```

[Live example](https://jscomplete.com/playground/s789980)

`useReducer` overcomplicates a simple counter, but is very handy when you need to coordinate global state shared across an application.

## Assignment: Move the todo items to global state with a reducer

Use React Context and `useReducer` to move the todo item state and logic to the main `App` component. Since the state will be stored in a parent component of the routes, the todo data will be not be lost when navigating back and forth between app pages.

> **Note:** reducer functions must be pure functions since React might call the reducer function more than once for a single action. If you are saving arrays and objects in state, make sure to make deep copies before mutating the data. Do not modify the state object directly.
