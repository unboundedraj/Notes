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

```javascript
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

## What is the difference between Mounting, Updating, and Unmounting in React?

These are the three major phases of a component's lifecycle.

1. Mounting: The component is created and added to the DOM for the first time.
2. Updating: The component re-renders when its state or props change.
3. Unmounting: The component is removed from the DOM.

Example using useEffect():

```javascript
function User() {
  useEffect(() => {
    console.log("Component Mounted");

    return () => {
      console.log("Component Unmounted");
    };
  }, []);

  return <h1>User Component</h1>;
}
```

- The effect runs after the component mounts.
- The cleanup function runs when the component unmounts.

Class component lifecycle methods:


| Lifecycle Phase | Method                   |
| --------------- | ------------------------ |
| Mounting        | `componentDidMount()`    |
| Updating        | `componentDidUpdate()`   |
| Unmounting      | `componentWillUnmount()` |


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

## What is Babel, why is it important in modern web development, and how does it function, configure, and integrate with tools like Webpack and React?

**Babel** is a popular JavaScript compiler that translates modern JavaScript (ES6 and beyond) and JSX into backwards-compatible versions (like ES5) that can run smoothly in older browsers or environments.

#### **Key Functions &amp; Capabilities**

- **Transpiling Modern Syntax:** Converts modern features like arrow functions, template literals, and destructuring into older, supported equivalents.
- **Polyfilling:** Simulates features missing natively in older environments (such as `Promises` or `async/await`) using tools like **core-js** and **regenerator-runtime**.
- **Experimental Features:** Allows developers to test cutting-edge ECMAScript proposals before official standardization.
- **React JSX Transformation:** Converts React's HTML-like JSX syntax into plain, browser-compatible JavaScript.

#### **Importance**

Babel provides **browser compatibility** across different environments, offers **development convenience** by automating code transformation, and ensures **ecosystem support** for upcoming language features.

#### **How It Works &amp; Configuration**

Babel operates during a project's build process by processing source code through **presets** (collections of plugins, such as `@babel/preset-env` for target browsers and `@babel/preset-react` for JSX) and individual **plugins** (for specific syntax transformations).

#### **Integration with Webpack**

Babel is commonly paired with bundlers like Webpack. In this workflow, Webpack processes and bundles project files while Babel transpiles the modern syntax, resulting in a single, fully compatible final JavaScript bundle.

## What is the difference between Functional Components and Class Components?


| Functional Components                        | Class Components                                       |
| -------------------------------------------- | ------------------------------------------------------ |
| JavaScript functions.                        | ES6 JavaScript classes.                                |
| Use Hooks for state and side effects.        | Use lifecycle methods.                                 |
| No `this` keyword required.                  | Often use `this` to access state and methods.          |
| Generally simpler and more concise.          | More verbose syntax.                                   |
| Cannot directly use class lifecycle methods. | Supports lifecycle methods like `componentDidMount()`. |


Functional Component:

```javascript
function Welcome() {
  const [name, setName] = useState("John");

  return <h1>Hello {name}</h1>;
}
```

Class Component:

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
function useCounter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(prev => prev + 1);
  };

  return { count, increment };
}
```

Using the custom Hook:

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
const UserContext = createContext();

<UserContext.Provider value={user}>
  <App />
</UserContext.Provider>
```

Redux Toolkit example:

```javascript
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

## What is the difference between Debouncing and Throttling? How would you implement them in React?

Both are techniques used to control how frequently a function executes.

Debouncing: Delays function execution until the user stops triggering an event for a specified period.

Example: Search suggestions should appear after the user stops typing for 500ms.

Throttling: Ensures a function executes at most once within a specified time interval, regardless of how frequently an event occurs.

Example: Limiting scroll event handling to once every 500ms.


| Debouncing                       | Throttling                           |
| -------------------------------- | ------------------------------------ |
| Executes after the event stops.  | Executes at controlled intervals.    |
| Resets the timer on every event. | Limits execution frequency.          |
| Useful for search inputs.        | Useful for scroll and resize events. |


Debouncing implementation:

```javascript
function Search() {
  const [query, setQuery] = useState("");

  useEffect(() => {
    const timer = setTimeout(() => {
      console.log("API Call:", query);
    }, 500);

    return () => clearTimeout(timer);
  }, [query]);

  return (
    <input
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      placeholder="Search..."
    />
  );
}
```

Here, the API call executes only when the user stops typing for 500ms.

Throttling implementation:

```javascript
function handleScroll() {
  console.log("Scroll event triggered");
}

useEffect(() => {
  let lastExecution = 0;

  const throttledScroll = () => {
    const now = Date.now();

    if (now - lastExecution >= 500) {
      handleScroll();
      lastExecution = now;
    }
  };

  window.addEventListener("scroll", throttledScroll);

  return () => {
    window.removeEventListener("scroll", throttledScroll);
  };
}, []);
```

## What are React's Synthetic Events? How are they different from Native DOM Events?

Synthetic Events are React's cross-browser event objects that provide a consistent interface for handling events across different browsers.

React wraps native browser events in its SyntheticEvent system, exposing properties and methods similar to native DOM events.

Example:

```cpp
function App() {
  const handleClick = (event) => {
    console.log(event.type);
    console.log(event.target);
  };

  return (
    <button onClick={handleClick}>
      Click Me
    </button>
  );
}
```

Here, `event` is a React SyntheticEvent.

Difference:


| Synthetic Events                       | Native DOM Events                      |
| -------------------------------------- | -------------------------------------- |
| Provided through React event handling. | Provided directly by the browser.      |
| Offers a consistent event interface.   | Browser-native event interface.        |
| Handled through React's event system.  | Handled through DOM event APIs.        |
| Accessed through props like `onClick`. | Registered using `addEventListener()`. |


Important points:

- React event names use camelCase, such as `onClick` and `onChange`.
- React events generally bubble through the React component tree.
- Use `event.nativeEvent` to access the underlying native event.
- Modern React does not pool SyntheticEvent objects, so `event.persist()` is generally unnecessary.

## How would you prevent unnecessary API calls when a user types into a search input?

We can use Debouncing to prevent API calls on every keystroke. Instead, we wait for the user to stop typing for a specified duration before making the API request.

Example:

```javascript
function Search() {
  const [search, setSearch] = useState("");
  const [results, setResults] = useState([]);

  useEffect(() => {
    if (!search.trim()) {
      setResults([]);
      return;
    }

    const controller = new AbortController();

    const timer = setTimeout(async () => {
      try {
        const response = await fetch(
          `/api/search?q=${encodeURIComponent(search)}`,
          { signal: controller.signal }
        );

        if (!response.ok) {
          throw new Error("API request failed");
        }

        const data = await response.json();
        setResults(data);
      } catch (error) {
        if (error.name !== "AbortError") {
          console.error(error);
        }
      }
    }, 500);

    return () => {
      clearTimeout(timer);
      controller.abort();
    };
  }, [search]);

  return (
    <>
      <input
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        placeholder="Search..."
      />

      {results.map(item => (
        <p key={item.id}>{item.name}</p>
      ))}
    </>
  );
}
```

How it works:

1. User enters text.
2. A 500ms timer starts.
3. If the user types again, the previous timer is cleared.
4. Once the user stops typing, the API request executes.
5. If a previous request is still running, it is aborted when the effect cleans up.

This reduces unnecessary API requests and helps avoid displaying outdated search results.

## How would you identify and fix unnecessary re-renders in a React application?

Unnecessary re-renders occur when components execute again even though their output does not need to change.

How to identify them:

- React DevTools Profiler: Identifies which components render and how much time they take.
- React DevTools Components: Helps inspect component props, state, and context.
- Console logs: Can help identify unexpected component executions.

Ways to optimize:

1. `React.memo()` – Prevents re-rendering when props remain shallowly equal.
2. `useMemo()` – Memoizes expensive calculations.
3. `useCallback()` – Maintains stable function references.
4. Avoid unnecessary state updates.
5. Keep state close to the components that need it.
6. Split large components into smaller components.
7. Avoid unnecessary context updates.

Example:

Without memoization:

```
function Child({ name }) {
  console.log("Child rendered");

  return <h1>{name}</h1>;
}
```

Optimized using React.memo:

```
const Child = React.memo(({ name }) => {
  console.log("Child rendered");

  return <h1>{name}</h1>;
});
```

Now, if the parent re-renders but `name` remains shallowly equal, React can skip rendering the child.

Important: Re-rendering is not necessarily bad. Optimize only when profiling identifies an actual performance issue.

## What is the difference between Fetch and Axios? How do you handle API errors?

Both Fetch and Axios are used to make HTTP requests from JavaScript applications.


| Fetch                                           | Axios                                                              |
| ----------------------------------------------- | ------------------------------------------------------------------ |
| Built-in browser API.                           | Third-party HTTP library.                                          |
| Requires manual JSON parsing using `.json()`.   | Automatically parses JSON responses in common cases.               |
| Does not reject on HTTP errors like 404 or 500. | Rejects the promise for unsuccessful HTTP status codes by default. |
| Supports AbortController.                       | Supports AbortController.                                          |
| Interceptors are not built in.                  | Provides request and response interceptors.                        |


Fetch example:

```javascript
async function getUsers() {
  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error("Something went wrong");
    }

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error(error.message);
  }
}
```

Axios example:

```
import axios from "axios";

async function getUsers() {
  try {
    const response = await axios.get("/api/users");

    console.log(response.data);
  } catch (error) {
    console.error(error.response?.data || error.message);
  }
}
```

When to use what?

- Fetch: Suitable for simple API requests without additional dependencies.
- Axios: Useful for applications requiring interceptors, centralized configurations, and convenient request handling

## What are major drawbacks of Reactjs?

**1. It’s only the view layer**  
React doesn’t give you routing, data fetching, form handling, or global state out of the box. You have to pick and assemble these yourself (React Router, Redux/Zustand, React Query, etc.), which leads to “decision fatigue” and inconsistent project structures across teams.

**2. Steep, shifting learning curve**  
JSX, hooks, the rules of hooks, `useEffect` dependency arrays, memoization, and now server components all take time to understand. Hooks like `useEffect` are a common source of bugs (stale closures, infinite loops, unnecessary re-renders).

**3. Fast-changing ecosystem**  
Best practices keep moving: class components to hooks, Create React App being deprecated, the push toward frameworks like Next.js, and server components. Tutorials and libraries go out of date quickly.

**4. Poor SEO by default (client-side rendering)**  
A plain React SPA ships an almost empty HTML file and builds the page in the browser, which can hurt SEO and first-load performance. You typically need SSR/SSG via Next.js or Remix to fix this.

**5. Performance pitfalls**  
React’s re-rendering model means a state change can re-render large parts of the tree. Avoiding this requires manual optimization (`useMemo`, `useCallback`, `React.memo`), which adds complexity. The virtual DOM also adds overhead compared to compiler-based frameworks like Svelte or Solid.

**6. Bundle size**  
React plus ReactDOM adds baseline weight, and apps tend to grow heavy once you add routing, state libraries, and UI kits.

**7. Boilerplate and verbosity**  
Things like prop drilling, context setup, and Redux (especially older patterns) can involve a lot of repetitive code.

**8. JSX is a mixed blessing**  
Mixing markup and logic is powerful, but some developers dislike it, and it requires a build step (Babel/TypeScript/bundler).

## What is Flux?

Flux is Facebook’s architecture pattern for client-side apps, built around **unidirectional data flow**, so state changes are predictable and easy to debug in React apps.

**Four parts:**

- **Action**: plain object describing what happened (`{ type: "ADD_TODO" }`)
- **Dispatcher**: single central hub that sends every action to the stores
- **Store**: holds app state and updates it in response to actions
- **View**: React components that read from stores and trigger new actions

**Diagram:**

```
Action → Dispatcher → Store → View
   ↑                           |
   └─────── user interaction ──┘
```

## What is Redux ?

**Redux** is a predictable state management library for JavaScript apps, most commonly used with React. It keeps the entire application state in a single central **store**, and the state can only be changed by dispatching **actions**, which are handled by pure functions called **reducers**.  
**Redux is a predictable state container for JavaScript apps that manages global state through a single store, actions, and reducers, using unidirectional data flow.**

### Core concepts

- **Store**: a single object that holds the whole app state
- **Action**: a plain object describing what happened, e.g. `{ type: "INCREMENT" }`
- **Reducer**: a pure function `(state, action) => newState` that returns the updated state
- **Dispatch**: the method used to send an action to the store

### Flow

```
View → dispatch(Action) → Reducer → Store (new state) → View re-renders
```

### Small example

jsx

```jsx
import { createStore } from "redux";

function counterReducer(state = { count: 0 }, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

const store = createStore(counterReducer);
store.dispatch({ type: "INCREMENT" });
```

In React, the **react-redux** library connects components to the store using `useSelector` (read state) and `useDispatch` (send actions). Today, the recommended way to write Redux is **Redux Toolkit**, which reduces boilerplate.

### Three principles

1. **Single source of truth**: one store for the whole app
2. **State is read-only**: change it only by dispatching actions
3. **Changes are made with pure functions**: reducers
