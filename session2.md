# Session 2: Welcome to React

## Objectives

- Learn the basics of React
- Add Material UI components
- Assignment: Create a personal home page

## Learn the basics of React

[React](https://reactjs.org/) is a javascript library that makes it easier to write web apps. React apps are composed from "components", which are reusable UI building blocks.

```jsx
import React from "react";

const MyComponent = () => {
  return (
    <>
      <h1>Hello World!</h1>
      <p>I'm a React component.</p>
    </>
  );
};
```

[Live example](https://jscomplete.com/playground/s782557)

The best place to learn about React is their documentation. To get started, we need to understand the first 3 concepts:

- [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)
- [Rendering Elements](https://reactjs.org/docs/rendering-elements.html)
- [Components and Props](https://reactjs.org/docs/components-and-props.html)

> **Assignment:** Read the article ["Thinking in React"](https://reactjs.org/docs/thinking-in-react.html)

> **Recommended:** For more hands-on experience with React, follow this step-by-step [tutorial](https://reactjs.org/tutorial/tutorial.html).

## Add Material UI components

[Material UI](https://mui.com/) is an open source React component library that implements Google's [Material Design](https://material.io/design). Using a component library makes it easier to develop your application because you do not need to create the small building blocks that are required in every applicaiton. Instead of spending time building Buttons and Inputs for your app, you can import them from a component library and focus on developing new features for your users.

Each MUI component has 2 doc pages in the left-hand side bar. The "Components" section shows usage examples, and the "Component API" section lists the full set of supported properties. For example, this is the [Components/Button](https://mui.com/components/buttons/) page and this is the corresponding [Component API/Button](https://mui.com/api/button/) page.

### Install MUI as a dependency

To use Material UI components in your app, you need to install the npm packages required:

```
> npm install @mui/material @emotion/react @emotion/styled
```

MUI has a few other [required installation steps](https://mui.com/getting-started/installation/) to install the fonts and icons.

After going through the setup steps, check that you have the correct version installed:

```
> npm list @mui/material
```

It should print `v5.x.x`.

### Add a MUI component to your app

To use an installed dependency, you need to `import` it into the file.

Let's add a [MUI Button](https://mui.com/api/button/) to `/src/App.js`, the main React file in our app, by writing 2 new lines of Javascript:

```jsx
import { Button } from "@mui/material";
...
<Button variant="contained">Click me</Button>
```

Your `App.js` should look something like this now:

```jsx
import logo from "./logo.svg";
import "./App.css";
import { Button } from "@mui/material"; // new

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
        <Button variant="contained">Click me</Button> {/* new */}
      </header>
    </div>
  );
}

export default App;
```

To see the new Button in your app:

1. Save the file
2. run `npm start` again (because we added new npm dependencies)
3. `npm start` will open a new page at `localhost:3000` with your updates

It's even simpler to see your changes when you didn't just add new dependencies:

1. Save the file
2. refresh the browser page at `localhost:3000` to see your updates

## Assignment: Create a personal home page

Replace the current content of `App.js` and create a personal home page. Include details such as your name, a brief bio, hobbies, etc.

Use additional MUI components instead of basic `h` or `p` elements to make your page more interesitng.

Below is an example of what your home page might look like:

![Session 2 Complete](https://github.com/MiriamT/learn-react/blob/main/images/session2_complete.png?raw=true)
