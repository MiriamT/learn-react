# Session 7: Testing with React Testing Library

## Objectives

- What should we test?
- Testing React Components
- React Testing Library
- Assignment: Write tests for the Home, Todo, and Chat components

## What should we test?

Good tests simulate user behavior to test the things that users will care about.

Taking our `Todo` component as an example, we can use the assignment requirements as our base test cases:

1. A new todo item can be created with a custom `title`
2. All todo items are shown in a list
3. A todo item can be marked complete
4. A todo item can be deleted

Next we extend the test cases by determining the user actions required to perform those behaviors. The user actions will be specific to how you decided to implement each feature. Below are extended test cases to match the example implementation of Todo defined at the end of Session 3:

1. When a task title is typed into the input box and the 'add' button is clicked, a new todo item is added to the list
2. All added todo items are shown in a list
3. When a todo item's check icon is clicked, the item is marked complete
4. When a todo item's delete icon is clicked, the item is deleted from the list

After you have your base tests defined, you'll want to think about some edge cases too. Here are some more tests we should add to make sure our Todo app functions properly:

5. When no text is typed into the input box and the 'add' button is clicked, a todo item is not added to the list (prevent bad data)
6. When a task title is typed into the input box and the enter key is pressed, a new todo item is added to the list (alternate behaviors)
7. When the component first loads, no todo items are shown in the list (prevent bad data)
8. When a completed todo item's check icon is clicked, the item is marked uncomplete (additional feature)

Now that we know what we want to test, we can learn how to write tests for React components.

## Testing React Components

Writing tests is a 3 step process:

1. Setup an environment so that your component is ready to test the behavior
2. Simulate some user actions
3. Assert that your components did the "right thing" in response to the user actions

Sometimes the setup is just rendering your component in the test environment. In other cases, you need to do some more prep before you are ready to start your test case. For example, if you want to test that todos are shown in a list, you might need to add some todos as part of your setup step. If you are testing that a user can add a todo, then you would not add any todos in the setup step since that would be part of the user action.

React has a collection of good testing libraries which make it easy to test components. Before progressing to the next section read the following article to learn the basics:

> **Assignment:** Read [React Testing Recipes](https://reactjs.org/docs/testing-recipes.html)

## React Testing Library

React testing library improves 2 things over the traditional methods of testing React:

1. It simplifies test code through helpful utility methods
2. It improves test quality by testing changes in the DOM instead of changes in React components

> **Assignment:** Read the intro to [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)

React Testing Library is used together with [Jest](https://jestjs.io/docs/getting-started). Jest sets up the test environment and exectutes the tests and assertions, while React Testing Library simplifies the test logic.

### Simple Test

Below is a very simple test example using Jest and React Testing Library:

```jsx
import { render } from "@testing-library/react";

const Hello = (props) => <div>Hello {props.name}!</div>;

test("renders hello text based on the name prop", () => {
  const { getByText } = render(<Hello name="Miriam" />);
  const helloEl = getByText(/Hello/);
  expect(helloEl).toHaveTextContent("Hello Miriam!");
});
```

The test above renders the `Hello` component with a name prop, and checks that the text rendered in the `Hello` component matches the given name.

### Counter Test

We can also test components that change state based on user actions. For example, here are some tests for our `Counter` component defined in Session 3:

```jsx
import React, { useState } from "react";
import { render } from "@testing-library/react";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <div>Count: {count}</div>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
    </div>
  );
};

describe("Counter component", () => {
  test("starts the count label at 0", () => {
    const { getByText } = render(<Counter />);
    const countLabel = getByText(/Count/);
    expect(countLabel).toHaveTextContent("Count: 0");
  });

  test('increments the count label when the "+" button is clicked', () => {
    const { getByText } = render(<Counter />);
    const countLabel = getByText(/Count/);
    expect(countLabel).toHaveTextContent("Count: 0"); // initial condition

    const addButton = getByText(/\+/);
    addButton.click();
    expect(countLabel).toHaveTextContent("Count: 1");

    addButton.click();
    expect(countLabel).toHaveTextContent("Count: 2");
  });

  test('decrements the count label when the "-" button is clicked', () => {
    const { getByText } = render(<Counter />);
    const countLabel = getByText(/Count/);
    expect(countLabel).toHaveTextContent("Count: 0"); // initial condition

    const minusButton = getByText(/\-/);
    minusButton.click();
    expect(countLabel).toHaveTextContent("Count: -1");

    minusButton.click();
    expect(countLabel).toHaveTextContent("Count: -2");
  });
});
```

`describe()` groups a set of tests together. Then we declare 3 tests, each testing a different use case of the Counter component. To test its behavior, we simulate user actions by clicking the add or minus buttons and observing changes to the label text.

Note that **we do not directly interact with the props or state** of the `Counter` component. Props and state are internal implementation details. If we tested them directly, we would not be able to refactor our component without breaking tests. React Testing Library intentionally does not expose methods for manipulating the state of components to make sure tests focus on interacting with the DOM instead.

## Setting up Test files

Test files for a React component are defined in a separate file at the same level as the component level. They are named the same as the component file, but include `.test.` or `.spec.` to indicate that this file is a test file.

For example, `app.jsx` would have a matching `app.test.jsx` test file, and `todo.jsx` would have a matching `todo.test.jsx` test file.

## Tagging elements with a `data-testid` attribute

Sometimes it is helpful to tag elements with a `data-testid` attribute, so that you can locate them easier in your test. For example, you might need to get all of your todo items, so you can count them and check their values. You can't search on specific text, since each todo item is different. Instead you can mark all todo item elements with a `data-testid` attribute, and then query for all of the elements with a matching `data-testid` values.

```jsx
const TodoItem = (props) => {
  return <div data-testid="todo-item">{props.text}</div>;
};

/**
 * Gets all the todo items in the test environment.
 */
function getTodoItems() {
  const todoItemEls = screen.queryAllByTestId("todo-item");
  return todoItemEls.map((el) => el.textContent);
}
```

Read more here: https://testing-library.com/docs/queries/bytestid

## Assignment: Write tests for your app

1. Write **at least 3 tests** for the `App` component to test that clicking on the different Header buttons changes the page content
2. Write **at least 5 tests** for the `Todo` component to test the behaviors noted above.

A "test" is a `test()` block that may check multiple conditions to ensure the test condition passes for your component.

Each test file should be in the same folder as the corresponding component file, and be named the same as the component file with the suffix `.test.jsx`.

> **Note:** You may need to refactor your code to make it more modular and easier to test.

For example, you will need a Todo content in your test for the Todo component to function currectly. Refactoring the `TodoContext.Provider `into a new into a re-usable component named `TodoProvider` will allow you to use it in both your app code and the tests:

```jsx
import React, { useReducer } from "react";
import { todoReducer } from "./reducer";

export const TodoContext = React.createContext();

export const TodoProvider = (props) => {
  const [todoState, todoDispatch] = useReducer(todoReducer, {
    todos: [],
  });

  return (
    <TodoContext.Provider
      // context value has the todos state and also the dispatch function
      // so the todos can be updated from any part of the app
      value={{
        todos: todoState.todos,
        dispatch: todoDispatch,
      }}
    >
      {props.children}
    </TodoContext.Provider>
  );
};
```

Using the new `TodoProvider` in `App`:

```jsx
<TodoProvider>
  <Header pages={pages} navigate={useNavigate()} />
  <Routes>...</Routes>
</TodoProvider>
```

Using the new `TodoProvider` in the Todo tests:

```jsx
render(
  <TodoProvider>
    <Todo />
  </TodoProvider>
);
```

### Helpful articles

- https://testing-library.com/docs/react-testing-library/cheatsheet/
- https://testing-library.com/docs/example-react-router

![Session 7 Complete](https://github.com/MiriamT/learn-react/blob/main/images/session7_complete.png?raw=true)
