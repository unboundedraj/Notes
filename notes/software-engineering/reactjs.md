---
title: ReactJS
date: 2026-10-29
tags: [react]
---

## What is React, and what are its key features? Why is React called a library rather than a framework?

React is an open-source JavaScript library used to build dynamic and interactive user interfaces, particularly single-page applications (SPAs). It follows a component-based architecture, allowing developers to create reusable UI components  
Key features:

- Component-based architecture.
- Virtual DOM for efficient UI updates.
- Declarative UI development.
- One-way data binding (unidirectional data flow).
- Hooks for managing state and lifecycle-related behavior.
- Reusable components.

> React primarily handles the View layer of an application. Developers can independently choose routing, state management, API handling, and other tools. Frameworks generally provide more built-in structure and conventions for these things.

## What is the Virtual DOM? How does React use it to update the actual DOM efficiently?

The Virtual DOM is a lightweight JavaScript representation of the actual DOM. Whenever a component's state or props change, React creates an updated representation of the UI and compares it with the previous one through a process called reconciliation.

React identifies the required changes and commits the necessary updates to the actual DOM rather than unnecessarily rebuilding the entire DOM.

Example:

```cpp
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

When the count changes, React updates the relevant UI instead of manually recreating the entire page.

## What is the difference between Real DOM and Virtual DOM?


| Real DOM                                                 | Virtual DOM                                               |
| -------------------------------------------------------- | --------------------------------------------------------- |
| Represents the actual HTML document.                     | JavaScript representation of the UI.                      |
| Direct DOM manipulation can be expensive.                | Enables React to calculate necessary UI updates.          |
| Updating elements can trigger layout and rendering work. | Changes are calculated before being committed to the DOM. |
| Browser-managed structure.                               | React-managed representation.                             |
| Directly interacts with browser APIs.                    | Does not directly interact with the browser DOM.          |


Important: Virtual DOM does not automatically make every operation faster than direct DOM manipulation. Its primary benefit is enabling React to efficiently coordinate UI updates through reconciliation.

## What is JSX? How does JSX work internally, and why do we use it?

JSX stands for JavaScript XML. It is a syntax extension for JavaScript that allows us to write HTML-like markup inside JavaScript code.

Browsers cannot directly understand JSX, so it is transformed into JavaScript function calls by tools such as Babel or other build tools.

Example:

```
const element = <h1>Hello React</h1>;
```

It is transformed conceptually into:

```
const element = React.createElement(
  "h1",
  null,
  "Hello React"
);
```

With the modern JSX transform, it can instead compile to functions such as `_jsx()`.

### Why use JSX?

- Makes UI code readable.
- Allows JavaScript expressions inside markup using `{}`.
- Makes component composition easier.
- Keeps rendering logic and UI structure together.

## What is the difference between Functional Components and Class Components?


| Functional Components                        | Class Components                                       |
| -------------------------------------------- | ------------------------------------------------------ |
| JavaScript functions.                        | ES6 JavaScript classes.                                |
| Use Hooks for state and side effects.        | Use lifecycle methods.                                 |
| No `this` keyword required.                  | Often use `this` to access state and methods.          |
| Generally simpler and more concise.          | More verbose syntax.                                   |
| Cannot directly use class lifecycle methods. | Supports lifecycle methods like `componentDidMount()`. |


Functional Component:

```
function Welcome() {
  const [name, setName] = useState("John");

  return <h1>Hello {name}</h1>;
}
```

Class Component:

```
class Welcome extends React.Component {
  state = { name: "John" };

  render() {
    return <h1>Hello {this.state.name}</h1>;
  }
}
```

Functional components with Hooks are the recommended approach for modern React development. Class components are still supported.

## What is the difference between Props and State in React?

Props and State are both used to manage data in React, but they serve different purposes.


| Props                                                 | State                                  |
| ----------------------------------------------------- | -------------------------------------- |
| Passed from parent to child.                          | Managed inside a component.            |
| Read-only from the receiving component's perspective. | Can be updated using state setters.    |
| Used for component communication.                     | Used to manage dynamic component data. |
| Changes when the parent provides different values.    | Changes when its setter is called.     |


Example:

```cpp
function Child({ name }) {
  return <h1>Hello {name}</h1>;
}

function Parent() {
  const [name, setName] = useState("John");

  return (
    <>
      <Child name={name} />
      <button onClick={() => setName("David")}>
        Change Name
      </button>
    </>
  );
}
```

Here, `name` is state in the parent and a prop in the child.

## What is Prop Drilling? How can you avoid it?

Prop drilling is the process of passing data through multiple intermediate components just to make it available to a deeply nested child component.

It can make applications difficult to maintain when many components need the same data.

Example:

```
function App() {
  const user = "John";

  return <Parent user={user} />;
}

function Parent({ user }) {
  return <Child user={user} />;
}

function Child({ user }) {
  return <h1>{user}</h1>;
}
```

Ways to avoid prop drilling:

1. Context API – Share data across components without manually passing props through every level.
2. Redux – Centralized state management.
3. Zustand – Lightweight global state management.
4. Component composition – Pass components as children or props to reduce unnecessary data passing.

## What is the difference between Controlled and Uncontrolled Components?

These concepts primarily refer to how form elements manage their values in React.

Controlled Components: Form data is managed by React state. Every change updates the state through an event handler.

```cpp
function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

Uncontrolled Components: Form data is managed by the DOM itself. React accesses the value when needed using a ref.

```cpp
function Form() {
  const inputRef = useRef(null);

  const handleSubmit = () => {
    alert(inputRef.current.value);
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```


| Controlled                              | Uncontrolled                                 |
| --------------------------------------- | -------------------------------------------- |
| Uses React state.                       | Uses DOM to manage values.                   |
| Uses `value` and `onChange`.            | Commonly uses `defaultValue` and refs.       |
| Provides better control and validation. | Useful for simpler form handling.            |
| State updates can trigger re-renders.   | Typing does not require React state updates. |


## Why are Keys Important When Rendering Lists in React? Why avoid array indexes as keys?

Keys are unique identifiers assigned to elements when rendering lists. React uses keys to identify which items have been added, removed, or modified during reconciliation.

Example:

```
const users = [
  { id: 1, name: "John" },
  { id: 2, name: "David" }
];

function UserList() {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

Why avoid array indexes?

When list items are added, removed, or reordered, indexes can change. React may then associate existing component state or DOM elements with the wrong list items.

Best practices:

- Use unique and stable IDs.
- Avoid random values as keys.
- Avoid indexes when list order can change.
- Indexes are acceptable for static lists that never change order or length.

## What is Component Re-rendering? What are the different reasons a React component re-renders?

Re-rendering means React executes a component again to calculate its updated UI. React then reconciles the new output with the previous one and commits necessary changes.

Common reasons for re-rendering:

1. State change: A component's state setter is called with a different value.
2. Props change: The parent provides different props.
3. Parent re-render: A parent re-renders, and its children may also re-render.
4. Context change: A context value consumed by the component changes.
5. External store update: A subscribed external store notifies the component.

Example:

```
function Counter() {
  const [count, setCount] = useState(0);

  console.log("Component rendered");

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

Every time the count changes, React re-renders the component.

Important: A re-render does not necessarily mean the actual DOM will be updated. React may determine that no DOM changes are required.  


## What are React Hooks? Why were they introduced?

Hooks are special functions introduced in React 16.8 that allow functional components to use React features such as state, context, refs, and effects.

Before Hooks, stateful logic and lifecycle methods were primarily handled using class components.

Common Hooks:

- `useState()` – Manage component state.
- `useEffect()` – Synchronize with external systems.
- `useContext()` – Access context values.
- `useRef()` – Store mutable values and access DOM elements.
- `useMemo()` – Cache calculated values.
- `useCallback()` – Cache function definitions.

### Why were Hooks introduced?

- To reuse stateful logic through custom Hooks.
- To avoid complex class component structures.
- To reduce dependence on HOCs and Render Props for logic reuse.
- To simplify component organization.

Rules of Hooks:

1. Only call Hooks at the top level, not inside loops, conditions, or nested functions.
2. Only call Hooks from React function components or custom Hooks.

## Explain useState() and how state updates work in React.

`useState()` is a React Hook used to add and manage state inside functional components.

It returns an array containing the current state value and a setter function used to update it.

Syntax:

```
const [state, setState] = useState(initialValue);
```

Example:

```
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </>
  );
}
```

How state updates work:

- Calling the setter schedules an update.
- React processes the update and re-renders the component.
- State updates are often batched for better performance.
- State behaves as a snapshot within a particular render.

Functional state update:

When the next state depends on the previous state, use the functional updater form.

```
setCount(prevCount => prevCount + 1);
```

For example:

```
setCount(count + 1);
setCount(count + 1);
```

These two calls do not necessarily increment the count twice because both use the same render's state snapshot.

Instead:

```
setCount(prev => prev + 1);
setCount(prev => prev + 1);
```

This correctly increments the count twice.

## Explain useEffect() and its dependency array. What is the difference between useEffect() and useLayoutEffect()?

`useEffect()` is a React Hook used to synchronize a component with external systems, such as API calls, subscriptions, timers, and event listeners.

Syntax:

```
useEffect(() => {
  // Side effect

  return () => {
    // Cleanup
  };
}, [dependencies]);
```

Different dependency configurations:


| Dependency          | Behaviour                                        |
| ------------------- | ------------------------------------------------ |
| No dependency array | Runs after every committed render.               |
| `[]`                | Runs after the initial mount.                    |
| `[count]`           | Runs after initial mount and when count changes. |


Example:

```
useEffect(() => {
  console.log("Count changed:", count);
}, [count]);
```

Difference between useEffect and useLayoutEffect:


| useEffect                                         | useLayoutEffect                                                            |
| ------------------------------------------------- | -------------------------------------------------------------------------- |
| Runs after the browser has had a chance to paint. | Runs synchronously after DOM mutations but before browser paint.           |
| Does not block painting in normal cases.          | Can block browser painting.                                                |
| Used for API calls, subscriptions, etc.           | Used when DOM measurements or layout adjustments must happen before paint. |


Example of useLayoutEffect:

```
useLayoutEffect(() => {
  const height = ref.current.offsetHeight;
  console.log(height);
}, []);
```

Use `useEffect()` by default. Use `useLayoutEffect()` only when you need to measure or synchronously adjust layout before the browser paints.

## What is the purpose of the Cleanup Function in useEffect()?

The cleanup function is used to remove or undo side effects created inside an effect. It helps prevent memory leaks, duplicate subscriptions, and unwanted background operations.

React executes cleanup:

- Before running an effect again when its dependencies change.
- When the component unmounts.

Example:

```
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running...");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

Here, `clearInterval()` stops the timer when the component unmounts.

Other common use cases:

- Removing event listeners.
- Unsubscribing from subscriptions.
- Aborting API requests.
- Clearing timeouts and intervals.

## What is useRef()? How is it different from useState()?

`useRef()` is a React Hook used to store mutable values that persist across renders without triggering a re-render when changed. It is also commonly used to access DOM elements directly.

Example – DOM access:

```cpp
function Input() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus</button>
    </>
  );
}
```

Difference between useState and useRef:


| useState                                                    | useRef                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------- |
| Stores component state.                                     | Stores mutable values.                                        |
| Updating state triggers a re-render when the value changes. | Updating `ref.current` does not trigger a re-render.          |
| Used for values displayed in UI.                            | Used for DOM references and values that don't need rendering. |
| State updates are scheduled.                                | Ref updates are immediate mutations.                          |


## What is the difference between useMemo() and useCallback()?

Both Hooks are used for performance optimization by caching values between renders.

useMemo(): Caches the result of a calculation and recalculates it only when dependencies change.

```
const expensiveValue = useMemo(() => {
  return items.reduce((sum, item) => sum + item.price, 0);
}, [items]);
```

useCallback(): Caches a function definition and returns the same function reference until its dependencies change.

```
const handleClick = useCallback(() => {
  console.log("Button clicked");
}, []);
```

Difference:


| useMemo                            | useCallback                                   |
| ---------------------------------- | --------------------------------------------- |
| Memoizes a calculated value.       | Memoizes a function reference.                |
| Returns the result of a function.  | Returns the function itself.                  |
| Useful for expensive calculations. | Useful when stable function identity matters. |


Easy way to remember:

- `useMemo` → Memoizes a value.
- `useCallback` → Memoizes a function.

Both should be used when they provide a measurable or meaningful performance benefit, not everywhere.

## What is useContext()? How does the Context API help with State Management?

`useContext()` is a React Hook that allows components to access values provided by a Context without passing props manually through every intermediate component.

It helps solve prop drilling and is useful for sharing global or application-level data.

Example:

```
import { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}

function Child() {
  const theme = useContext(ThemeContext);

  return <h1>Current Theme: {theme}</h1>;
}
```

Common use cases:

- Authentication information.
- Theme management.
- Language preferences.
- Application-level configuration.

Important: Context is a way to distribute data, not a complete replacement for every state management solution. Frequent context updates can cause many consuming components to re-render.

## What are Custom Hooks? Why and when should you create them?

Custom Hooks are JavaScript functions whose names start with `use` and which can call other React Hooks. They allow developers to reuse stateful logic across multiple components.

Example:

```
function useCounter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(prev => prev + 1);
  };

  return { count, increment };
}
```

Using the custom Hook:

```
function Counter() {
  const { count, increment } = useCounter();

  return (
    <>
      <h1>{count}</h1>
      <button onClick={increment}>
        Increment
      </button>
    </>
  );
}
```

### Why use Custom Hooks?

- Reuse stateful logic.
- Keep components clean and maintainable.
- Separate business logic from UI.
- Avoid duplicating logic across components.

Important: Custom Hooks share logic, not the same state instance. Each component calling a custom Hook gets its own independent Hook state unless the logic uses a shared external store or context.

## What is Reconciliation in React? How does React's Diffing Algorithm Work?

Reconciliation is the process React uses to compare the previous UI representation with the new one and determine what changes need to be applied to the actual DOM.

React uses its diffing algorithm to identify differences efficiently rather than rebuilding the entire UI.

How it works:

1. React renders the component and creates a new element tree.
2. React compares the new tree with the previous tree.
3. It identifies elements that have changed.
4. It uses element types, positions, and keys to determine whether elements can be reused.
5. React commits the necessary DOM changes.

Important rules:

- Different element types generally result in the old subtree being replaced.
- Elements of the same type can be updated while preserving their DOM identity.
- Keys help React identify corresponding elements in lists.

Example:

```
function App() {
  const [show, setShow] = useState(false);

  return (
    <>
      {show ? <h1>Hello</h1> : <h1>Welcome</h1>}

      <button onClick={() => setShow(!show)}>
        Toggle
      </button>
    </>
  );
}
```

Here, React can reuse the existing `h1` DOM element and update its text instead of replacing the entire element.

## What are Higher-Order Components (HOCs) and Render Props?

Both are patterns used to share reusable component logic in React.

Higher-Order Component (HOC):

A Higher-Order Component is a function that takes a component as an argument and returns an enhanced component with additional functionality.

```
function withAuth(Component) {
  return function EnhancedComponent(props) {
    const isLoggedIn = true;

    if (!isLoggedIn) {
      return <h1>Please Login</h1>;
    }

    return <Component {...props} />;
  };
}

function Dashboard() {
  return <h1>Welcome to Dashboard</h1>;
}

const ProtectedDashboard = withAuth(Dashboard);
```

Render Props:

Render Props is a pattern where a component receives a function as a prop and calls that function to determine what UI should be rendered.

```
function DataProvider({ render }) {
  const data = "Hello React";

  return render(data);
}

function App() {
  return (
    <DataProvider
      render={(data) => <h1>{data}</h1>}
    />
  );
}
```

Difference:


| HOC                                                  | Render Props                                     |
| ---------------------------------------------------- | ------------------------------------------------ |
| Takes a component and returns an enhanced component. | Uses a function prop to render UI.               |
| Shares functionality through component wrapping.     | Shares functionality through function callbacks. |
| Can lead to wrapper nesting.                         | Can lead to nested callback structures.          |


Custom Hooks are generally preferred for sharing stateful logic in modern React applications.

## What is Lazy Loading in React? Explain React.lazy() and Suspense.

Lazy loading is a technique where components or resources are loaded only when required rather than loading everything during the initial application load.

React provides `React.lazy()` and `Suspense` to implement component-level lazy loading.

Example:

```
import { lazy, Suspense } from "react";

const Dashboard = lazy(
  () => import("./Dashboard")
);

function App() {
  return (
    <Suspense fallback={<h2>Loading...</h2>}>
      <Dashboard />
    </Suspense>
  );
}
```

### How it works:

- `React.lazy()` dynamically imports the component.
- The component's code is loaded when React attempts to render it.
- `Suspense` displays fallback UI while the component is loading.
- Once loaded, React renders the actual component.

Benefits:

- Reduces initial JavaScript bundle size.
- Improves initial loading performance.
- Supports code splitting.
- Useful for routes and large components.

## What is the Difference Between Client-Side Rendering (CSR) and Server-Side Rendering (SSR)?

CSR and SSR are two approaches used to render web applications.

Client-Side Rendering (CSR):

The browser downloads JavaScript and executes it to generate the UI. React applications commonly use CSR when built as traditional single-page applications.

Server-Side Rendering (SSR):

The server generates the initial HTML and sends it to the browser. React can then hydrate that HTML to make it interactive.


| CSR                                               | SSR                                                                         |
| ------------------------------------------------- | --------------------------------------------------------------------------- |
| UI is primarily rendered in the browser.          | Initial HTML is generated on the server.                                    |
| Initial content may depend on JavaScript loading. | Initial content can be displayed before client JavaScript finishes loading. |
| Less server rendering work.                       | Requires server-side rendering infrastructure.                              |
| Can require additional SEO considerations.        | Can improve initial content availability for search engines.                |
| Common in traditional React SPAs.                 | Supported by frameworks such as Next.js.                                    |


Important: SSR and hydration are not the same thing. SSR generates HTML on the server, while hydration attaches React's event handling and interactivity to the existing server-rendered HTML.

## What is the Difference Between Context API, Redux, and Zustand?

All three are used to share and manage application state, but they have different approaches.


| Context API                                                 | Redux Toolkit                                         | Zustand                                               |
| ----------------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| Built into React.                                           | External state management library.                    | Lightweight external state management library.        |
| Uses Providers and `useContext()`.                          | Uses a centralized store and reducers.                | Uses a centralized store with hooks.                  |
| Suitable for shared application data.                       | Suitable for complex state management.                | Suitable for simple to complex shared state.          |
| No built-in middleware system.                              | Supports middleware and DevTools ecosystem.           | Supports middleware and DevTools integration.         |
| Context consumers can re-render when context values change. | Uses subscriptions and selectors to optimize updates. | Uses selectors to subscribe to specific state slices. |


Context API example:

```cpp
const UserContext = createContext();

<UserContext.Provider value={user}>
  <App />
</UserContext.Provider>
```

Redux Toolkit example:

```cpp
const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    }
  }
});
```

Zustand example:

```cpp
const useStore = create((set) => ({
  count: 0,
  increment: () =>
    set((state) => ({
      count: state.count + 1
    }))
}));
```

### When to use what?

- Context API: Theme, authentication, language preferences.
- Redux Toolkit: Complex application state, predictable update patterns, middleware requirements.
- Zustand: Lightweight global state with minimal boilerplate.

## How Would You Optimize the Performance of a Slow React Application?

React application performance can be improved by reducing unnecessary renders, optimizing expensive calculations, and minimizing the amount of JavaScript and UI work.

Important optimization techniques:

1. React.memo(): Prevents unnecessary re-rendering of a component when its props remain shallowly equal.
2. useMemo(): Memoizes expensive calculations.
3. useCallback(): Maintains stable function references when useful.
4. Code Splitting: Load components only when required using `React.lazy()` and `Suspense`.
5. List Virtualization: Render only visible list items instead of rendering thousands of elements simultaneously.
6. Avoid Unnecessary State: Keep state as close as possible to the components that need it.
7. Optimize Images: Use appropriate formats, compression, and lazy loading.
8. Debouncing and Throttling: Reduce unnecessary event-handler executions.
9. Proper Keys: Use stable keys when rendering lists.
10. Profiling: Use React DevTools Profiler to identify unnecessary renders and performance bottlenecks.

Example – React.memo():

```
const Child = React.memo(({ name }) => {
  console.log("Child rendered");

  return <h1>{name}</h1>;
});
```

React can skip rendering `Child` when its props remain shallowly equal.

Interview tip: Always identify the actual performance bottleneck using profiling before applying optimization techniques.
