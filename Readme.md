# React Interview Questions

# React Interview Questions and Answers

## What is React?

React is a JavaScript library for building user interfaces, particularly for single-page applications. It allows developers to create reusable UI components and manage the state of their applications efficiently, making it easier to build dynamic and responsive web applications.

## What are the features of React?

### 1. Component-Based Architecture

- React applications are built using reusable components.
- Each component has its own logic and UI, making the code modular and easier to manage.

### 2. Virtual DOM (VDOM)

- React uses a Virtual DOM to improve performance.
- Instead of updating the actual DOM directly, it first updates the Virtual DOM and then efficiently applies changes to the real DOM using a diffing algorithm.

### 3. JSX (JavaScript XML)

- JSX is a syntax extension for JavaScript that looks similar to HTML.
- It allows developers to write UI elements in a declarative way inside JavaScript code.

### 4. One-Way Data Binding

- React follows a unidirectional data flow.
- Data flows from parent components to child components via props, ensuring better control over application state.

### 5. State Management

- React provides a built-in `useState` hook for managing local component states.
- For complex applications, context API, Redux, or Zustand can be used for global state management.

### 6. Performance Optimization

- React optimizes performance using techniques like:
  - Memoization (`React.memo`, `useMemo`, `useCallback`)
  - Code Splitting (`lazy` & `Suspense`)
  - Reconciliation (efficient diffing algorithm for updating UI)

### 7. Cross-Platform Development

- React Native allows React code to be used for mobile applications.
- Enables building cross-platform apps with a single codebase.

### 8. Strong Community Support & Ecosystem

- React has a vast ecosystem of libraries and tools.
- It is maintained by Facebook (Meta) and has a strong developer community.

## What is JSX? Why can't browsers understand JSX?

JSX (JavaScript XML) is a syntax extension for JavaScript that allows you to write HTML-like code directly within JavaScript files. It makes it easier to create and visualize the structure of user interfaces in React.

### Why Browsers Can't Understand JSX?

- Web browsers cannot read JSX because JSX is not valid JavaScript that browsers can interpret directly.
- JSX needs to be transpiled (converted) into standard JavaScript using tools like Babel.

#### JSX Code Example:

```jsx
const element = <h1>Hello, World!</h1>;
```

This code gets converted by Babel into:

```js
const element = React.createElement("h1", null, "Hello, World!");
```

## What is State in React?

State is a built-in object used to store dynamic data or information that can change over time. When the state of a component changes, React re-renders the component to reflect the updated state in the UI.

### Example of State in React:

```jsx
import React, { useState } from "react";
function Counter() {
  const [count, setCount] = useState(0);
  const increment = () => setCount(count + 1);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
export default Counter;
```

## What are Props in React?

Props (short for properties) are the mechanism React uses to pass data from a parent component to a child component. Props are read-only, meaning that a child component cannot modify the props it receives. Instead, props are used to render dynamic data or pass configuration/settings to child components.

### Example of Props in React:

```jsx
import React from "react";
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
function App() {
  return <Greeting name="John" />;
}
export default App;
```

## Difference Between State and Props

| State                                                                                     | Props                                                                   |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Local data store within a component, used to keep track of changing data.                 | Data passed from a parent component to a child component.               |
| Can be modified by the component itself and causes re-renders when updated.               | Read-only; cannot be modified by the child component.                   |
| Mutable: data can be updated using state update functions (e.g., `setState`, `useState`). | Immutable within the child component; the parent must modify the props. |
| Managed within the component.                                                             | Managed by the parent component.                                        |
| Used for data that changes over time.                                                     | Used to pass data to child components.                                  |

## Difference between Functional Component and Class-Based Component

| Functional Components                                                                                | Class Components                                                                    |
| ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| A plain JavaScript function that takes props as input and returns JSX.                               | A JavaScript class that extends `React.Component` and requires a `render()` method. |
| Originally stateless, but now manages state using hooks like `useState`.                             | Manages state using `this.state` and updates it with `this.setState()`.             |
| Cannot use traditional lifecycle methods, but uses hooks like `useEffect` for similar functionality. | Can use lifecycle methods like `componentDidMount`, `componentDidUpdate`, etc.      |
| Easier to write and understand. No need for a `render()` method or a constructor.                    | More verbose and requires a constructor to initialize state.                        |

## Virtual DOM

The Virtual DOM is essentially a lightweight copy of the real DOM. It's a virtual representation of the UI components in the form of JavaScript objects. These objects reflect the structure of the actual DOM but without the complexity and performance overhead of manipulating the real DOM directly.

### How It Works:

1. **Initial Render:**

   - When the application starts, React creates a virtual DOM that represents the entire UI.
   - Each element in the virtual DOM is a plain JavaScript object that contains the structure of the component.

2. **State or Prop Changes:**

   - React first updates the virtual DOM representation before touching the real DOM.
   - The updated virtual DOM is a new tree reflecting the changes in state or props.

3. **Diffing Algorithm:**

   - React uses a process called reconciliation to compare the current virtual DOM tree with the previous version.
   - The diffing algorithm identifies the minimal number of changes needed.

4. **Batching Updates:**

   - React batches updates to optimize performance and reduce unnecessary reflows or repaints.

5. **Re-rendering the Real DOM:**
   - The real DOM is updated with the minimal set of changes required, ensuring efficient rendering.

### Why the Virtual DOM?

- **Performance Optimization:** Minimizes direct DOM manipulation, reducing reflows and repaints.
- **Declarative UI Updates:** Ensures that React efficiently manages updates.

---

## One-Way Data Binding

One-way data binding in React means that data flows in only one direction — from the parent component to the child component.

### How One-Way Data Binding Works:

1. **State in Parent Component:** Stores data.
2. **Passing Data as Props:** Parent passes state to child via props.
3. **Triggering Updates:** Parent updates its state, and React re-renders components accordingly.

```jsx
import React, { useState } from "react";
function ParentComponent() {
  const [message, setMessage] = useState("Hello, World!");
  const changeMessage = () => setMessage("Hello, React!");

  return (
    <div>
      <ChildComponent message={message} />
      <button onClick={changeMessage}>Change Message</button>
    </div>
  );
}
function ChildComponent({ message }) {
  return <h1>{message}</h1>;
}
export default ParentComponent;
```

### Why One-Way Data Binding is Useful:

- **Predictable**: Clear data flow.
- **Easy to Debug**: Changes are traceable.
- **Reusable Components**: More modular structure.

---

## Lifting State Up

Lifting state up means moving state from a child component to its parent so multiple components can share it.

### Example:

```jsx
import React, { useState } from "react";
function ParentComponent() {
  const [count, setCount] = useState(0);
  const incrementCount = () => setCount(count + 1);

  return (
    <div>
      <ChildComponent count={count} increment={incrementCount} />
    </div>
  );
}
function ChildComponent({ count, increment }) {
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
export default ParentComponent;
```

### When to Lift State Up:

- When two or more components need to share the same data.
- When managing shared data becomes complex.

---

## Conditional Rendering

Conditional rendering in React allows UI components to display different elements based on conditions.

### 1. Using if-else Statements

```jsx
function Welcome({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  } else {
    return <h1>Please log in.</h1>;
  }
}
```

### 2. Using Ternary Operator

```jsx
function Welcome({ isLoggedIn }) {
  return <h1>{isLoggedIn ? "Welcome back!" : "Please log in."}</h1>;
}
```

### 3. Logical AND (&&) Operator

```jsx
function Welcome({ isLoggedIn }) {
  return <div>{isLoggedIn && <h1>Welcome back!</h1>}</div>;
}
```

### 4. Switch Statements

```jsx
function Greeting({ status }) {
  switch (status) {
    case "logged-in":
      return <h1>Welcome back!</h1>;
    case "logged-out":
      return <h1>Please log in.</h1>;
    default:
      return <h1>Loading...</h1>;
  }
}
```

### 5. Rendering Multiple Components Conditionally

```jsx
function App() {
  const [isAdmin, setIsAdmin] = useState(false);
  return <div>{isAdmin ? <AdminDashboard /> : <UserDashboard />}</div>;
}
```

---

## The Key Prop in React

The `key` prop is used to uniquely identify elements in a list.

### Importance of `key`:

- **Efficient Reconciliation**: React identifies elements that have changed, been added, or removed.
- **Unique Identification**: Helps React track items across renders.
- **Optimized Virtual DOM Updates**: Improves performance.

### Example:

```jsx
const items = ["Apple", "Banana", "Cherry"];
function ItemList() {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}
```

**Best Practice:** Always use unique IDs for keys instead of indices when possible.

```jsx
const items = [
  { id: 1, name: "Apple" },
  { id: 2, name: "Banana" },
];
function ItemList() {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

---
