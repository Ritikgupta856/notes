# React.js — Interview Preparation Guide

## Table of Contents

1. [Introduction](#introduction)
2. [JSX](#jsx)
3. [Components](#components)
4. [Props](#props)
5. [State](#state)
6. [Hooks](#hooks)
7. [useEffect](#useeffect)
8. [Rendering](#rendering)
9. [Virtual DOM](#virtual-dom)
10. [Forms](#forms)
11. [Events](#events)
12. [Context API](#context-api)
13. [Zustand](#zustand)
14. [Routing](#routing)
15. [API Integration](#api-integration)
16. [Performance](#performance)
17. [Advanced React](#advanced-react)
18. [Project Structure](#project-structure)
19. [React Hooks Deep Dive](#react-hooks-deep-dive)
20. [Component Lifecycle](#component-lifecycle)
21. [Code Splitting](#code-splitting)

## Introduction

### 1. What is React? What is the Role of React in Software Development?
**Answer:** React is a JavaScript library developed by Facebook (Meta) for building user interfaces, specifically single-page applications. It allows developers to create reusable UI components that efficiently update and render when data changes. React's role is to provide a declarative, component-based approach to building interactive UIs where developers describe "what" the UI should look like rather than "how" to update it step by step.

### 2. What are the Key Features of React?
**Answer:**
- **Component-Based Architecture** — UI is built from small, reusable, self-contained components
- **Virtual DOM** — Uses an in-memory representation of the real DOM for efficient updates
- **Declarative Syntax** — JSX makes code readable; describe UI states and React handles DOM updates
- **Unidirectional Data Flow** — Data flows parent to child via props, making state predictable
- **Hooks** — Use state and lifecycle in functional components without classes
- **React Native** — Same concepts for mobile app development on iOS/Android
- **Rich Ecosystem** — Large community, libraries for routing, state management, forms, etc.

### 3. What is DOM? What is the difference between HTML and DOM?
**Answer:** DOM (Document Object Model) is a programming interface that represents the structure of an HTML document as a tree of objects. The browser creates the DOM after parsing HTML.

| HTML | DOM |
|------|-----|
| Static markup written by developer | Dynamic in-memory representation |
| Written in .html files | Created by browser at runtime |
| Cannot be manipulated directly via JavaScript | Can be queried and modified via JavaScript |
| Defines structure and content | Represents live document state |

### 4. What is SPA (Single Page Application)?
**Answer:** SPA is a web application that loads a single HTML page and dynamically updates content without full page reloads. JavaScript handles routing and content updates.

**Characteristics:**
- Only one initial page load from server
- Client-side routing (URL changes without page refresh)
- Faster navigation after initial load
- Better user experience (no white screen between pages)
- Examples: Gmail, Google Maps, Facebook, Twitter

**Trade-offs:**
- Pros: Fast interactions, reduced server load, better offline support
- Cons: Larger initial bundle, SEO challenges (mitigated by SSR), more memory usage

### 5. What are the 5 Advantages of React?
**Answer:**
1. **Reusable Components** — Build once, use everywhere; reduces code duplication
2. **Virtual DOM Performance** — Efficient updates by diffing and minimal real DOM manipulation
3. **Unidirectional Data Flow** — Predictable state management, easier debugging
4. **Rich Ecosystem & Community** — Thousands of libraries, active community, extensive documentation
5. **Cross-Platform** — React Native for mobile; React for web; same learning curve

### 6. What are the Disadvantages of React?
**Answer:**
1. **Rapid Changes** — Frequent updates require continuous learning
2. **Boilerplate** — Can require significant setup (though Vite simplifies this)
3. **JSX Learning Curve** — Mixing HTML in JavaScript feels unusual initially
4. **Bundle Size** — Large apps can have big bundles (mitigated by code splitting)
5. **Not Opinionated** — Lack of structure means developers must make architectural decisions (routing, state, etc.)

### 7. What is the difference between Declarative and Imperative Syntax?
**Answer:**

| Declarative (React) | Imperative (Vanilla JS) |
|---------------------|------------------------|
| Describe what the UI should look like | Describe step-by-step how to update UI |
| React handles DOM updates | Developer manually manipulates DOM |
| Readable, predictable | Verbose, error-prone |
| `return <button>{count}</button>` | `document.getElementById('btn').textContent = count` |

**Example:**
```jsx
// Declarative — React
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}

// Imperative — Vanilla JS
const btn = document.createElement('button');
let count = 0;
btn.addEventListener('click', () => {
  count++;
  btn.textContent = count;
});
document.body.appendChild(btn);
```

---

## JSX  
  
### 11. What is JSX?  
**Answer:** JSX stands for JavaScript XML. It is a syntax extension for JavaScript that allows us to write HTML-like code inside JavaScript. React uses JSX to describe what the UI should look like.  
  
### 12. Why use JSX?  
**Answer:** JSX makes component code easier to read and write because it lets us describe UI in a markup-like way inside JavaScript. Instead of manually calling `React.createElement`, JSX gives a cleaner, more expressive syntax.  
  
### 13. How does JSX work internally?  
**Answer:** JSX is not understood directly by the browser. It is transpiled by tools like Babel into `React.createElement()` calls or equivalent runtime functions. Those calls create plain JavaScript objects representing React elements, which React uses to build the Virtual DOM.  
  
### 14. JSX vs HTML?  
**Answer:** JSX looks similar to HTML, but it is not HTML. JSX is JavaScript syntax. It uses `className` instead of `class`, `htmlFor` instead of `for`, camelCase for event handlers like `onClick`, and expressions can be embedded using curly braces.  
  
### 15. Can JSX return multiple elements?  
**Answer:** Yes, but they must be wrapped in a single parent element, a Fragment, or an array. React components must return one logical root value.  
  
### 16. What are React Fragments?  
**Answer:** Fragments let us group multiple elements without adding an extra node to the DOM. They are useful when we want a clean DOM structure without unnecessary wrapper elements.  
  
### 17. Difference between Fragment and div?  
**Answer:** A `div` adds an actual element to the DOM, while a Fragment does not. So if I only need grouping for React rendering and not for styling or layout, I prefer Fragment.  
  
### 18. How is JSX converted into JavaScript?  
**Answer:** JSX is converted during build time by Babel or a similar compiler into JavaScript function calls. In older transforms it becomes `React.createElement`, and in newer transforms it may use optimized JSX runtime helpers.  
  
### 19. Why must components return one parent element?  
**Answer:** A component must return one parent because JavaScript functions return a single value. React needs a single root representation of the UI tree from that component. That root can contain children, but the return itself must be one unit.  
  
### 20. What are JSX expressions?  
**Answer:** JSX expressions are JavaScript expressions written inside curly braces in JSX. For example, we can render variables, conditions, array mappings, or function results directly inside the UI.  
  
### Q: What is an Arrow Function Expression in JSX?
**Answer:** Arrow functions provide a concise syntax for writing functions. In JSX, they're commonly used for inline event handlers and functional components.

```jsx
// Functional component with arrow function
const Welcome = ({ name }) => <h1>Hello, {name}</h1>;

// Inline event handler
<button onClick={() => setCount(count + 1)}>Click me</button>

// Conditional with arrow
const Greeting = ({ isLoggedIn }) => 
  isLoggedIn ? <h1>Welcome back</h1> : <h1>Please sign in</h1>;
```

### Q: What are the 5 Advantages of JSX?
**Answer:**
1. **Readable Syntax** — HTML-like structure is easier to understand than nested function calls
2. **Type Safety** — Expression interpolation `{}` catches errors at compile time
3. **Component Composition** — Clean markup for building complex UI trees
4. **No Template Injection** — Prevents XSS attacks (auto-escapes values)
5. **Developer Tools** — Better IDE support, syntax highlighting, and linting

### Q: What is Babel?
**Answer:** Babel is a JavaScript compiler/transpiler that converts modern JavaScript (ES6+) and JSX into browser-compatible JavaScript. In React, Babel transforms JSX into `React.createElement()` calls that browsers can execute.

```jsx
// JSX (what you write)
const element = <h1>Hello World</h1>;

// After Babel transpilation
const element = React.createElement('h1', null, 'Hello World');
```

### Q: What is the role of Fragment in JSX?
**Answer:** Fragments let you group multiple elements without adding an extra DOM node. They're useful when a component needs to return multiple elements but React requires a single parent.

```jsx
// Without Fragment — adds unnecessary div
function List() {
  return (
    <div>
      <h1>Title</h1>
      <p>Content</p>
    </div>
  );
}

// With Fragment — clean DOM
function List() {
  return (
    <>
      <h1>Title</h1>
      <p>Content</p>
    </>
  );
}
```

### Q: What is Spread Operator in JSX?
**Answer:** The spread operator `...` expands an object's properties into individual props. It's useful for passing all properties of an object as props to a component.

```jsx
// Object with props
const buttonProps = {
  type: 'submit',
  disabled: false,
  className: 'btn-primary'
};

// Spread all props
<button {...buttonProps}>Submit</button>

// Equivalent to
<button type="submit" disabled={false} className="btn-primary">Submit</button>

// Merge and override
<button {...buttonProps} disabled={true}>Submit</button>
```

### Q: What are the types of Conditional Rendering in JSX?
**Answer:**

```jsx
// 1. Ternary operator
{isLoggedIn ? <Dashboard /> : <Login />}

// 2. Logical AND (&&)
{message && <div>{message}</div>}

// 3. if/else with early return
function Greeting({ isLoggedIn }) {
  if (!isLoggedIn) return <Login />;
  return <Dashboard />;
}

// 4. switch statement (in separate function)
function getScreen(role) {
  switch(role) {
    case 'admin': return <AdminPanel />;
    case 'user': return <UserDashboard />;
    default: return <Login />;
  }
}

// 5. Variable assignment
let element;
if (condition) {
  element = <ComponentA />;
} else {
  element = <ComponentB />;
}
```

### Q: How do you iterate over a list in JSX? What is map() method?
**Answer:** The `map()` method transforms an array into JSX elements. Each item must have a unique `key` prop for React to track changes efficiently.

```jsx
const users = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
  { id: 3, name: 'Charlie' }
];

function UserList() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

### Q: Can a browser read a JSX file?
**Answer:** No. Browsers cannot read JSX directly. JSX must be transpiled by Babel (or similar tools) into standard JavaScript (`React.createElement` calls) before the browser can execute it. This is why React requires a build step.

### Q: What is Transpiler? What is the difference between Compiler and Transpiler?
**Answer:**
- **Compiler** converts source code from one language to another (e.g., C to machine code). May optimize.
- **Transpiler** converts source code from one language to another at the same abstraction level (e.g., ES6+ to ES5, JSX to JS).

Babel is a transpiler — it converts modern JavaScript/JSX into browser-compatible JavaScript without optimization. TypeScript compiler (tsc) is both — it type-checks and compiles.

### Q: Is it possible to use JSX without React?
**Answer:** Technically yes, JSX is just syntax that gets transpiled to function calls. You could use JSX with other libraries that provide `createElement`-like functions. However, JSX is designed for and tightly integrated with React. Without React, you'd need to provide your own runtime for the transpiled JSX output.

### Q: How to Setup React first project?
**Answer:**
```bash
# Using Vite (recommended)
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev

# Using Create React App (legacy)
npx create-react-app my-app
cd my-app
npm start
```

### Q: What is the difference between React and Angular?
**Answer:**

| Feature | React | Angular |
|---------|-------|---------|
| Type | Library | Full framework |
| Company | Meta (Facebook) | Google |
| Language | JavaScript/JSX | TypeScript |
| Architecture | Component-based | Component + Services + Modules |
| State | External (Context, Zustand) | Built-in (Services, RxJS) |
| Learning Curve | Lower | Higher |
| Bundle Size | Smaller | Larger |
| DOM | Virtual DOM | Real DOM (with change detection) |
| Data Flow | One-way | Two-way binding |
| Mobile | React Native | Ionic, NativeScript |

### Q: What are other 5 JS frameworks other than React?
**Answer:**
1. **Vue.js** — Progressive framework, easy learning curve
2. **Angular** — Full-featured enterprise framework by Google
3. **Svelte** — Compile-time framework, no virtual DOM
4. **Next.js** — React framework for SSR/SSG (built on React)
5. **Nuxt.js** — Vue framework for SSR/SSG

Others: Ember.js, Backbone.js, Alpine.js, Preact, SolidJS

### Q: Whether React is a Framework or a Library? What is the difference?
**Answer:** React is a **library**, not a framework. The difference:
- **Library** gives you tools to use as you choose (React handles UI only)
- **Framework** gives you a complete structure and enforces conventions (Angular has routing, HTTP, forms built-in)

React requires third-party libraries for routing (React Router), state management (Zustand/Redux), HTTP (Axios/fetch), etc. This flexibility is intentional — you choose your own tools.

---  
  
## Components  
  
### 21. What is a Component?  
**Answer:** A component is a reusable, self-contained piece of UI logic. It takes input through props, can manage internal state, and returns React elements describing what should be displayed.  
  
### 22. Functional vs Class Components?  
**Answer:** Functional components are plain JavaScript functions that return JSX. Class components use ES6 classes and lifecycle methods. Today, functional components are preferred because hooks give them the same capabilities with cleaner and simpler code.  
  
### 23. Why Functional Components are preferred?  
**Answer:** Functional components are preferred because they are easier to read, easier to test, less verbose, and work naturally with hooks. Hooks allow state, side effects, refs, and context without the complexity of class lifecycle methods.  
  
### 24. What is component composition?  
**Answer:** Component composition means building complex UIs by combining smaller components together. Instead of inheritance, React encourages composition, where components wrap or use other components to create flexible structures.  
  
### 25. What are reusable components?  
**Answer:** Reusable components are generic components designed to be used in multiple places with different data or behavior through props. For example, a Button, Modal, Input, or Card component.  
  
### 26. What are Higher Order Components (HOC)?  
**Answer:** A Higher Order Component is a function that takes a component and returns a new component with enhanced behavior. It is a pattern used to share logic, for example authentication checks or data injection.  
  
### 27. What is Render Props?  
**Answer:** Render Props is a pattern where a component shares logic by accepting a function as a prop, and that function returns UI. It gives flexibility because the parent controls what gets rendered using the data provided by the child.  
  
### 28. What is Compound Component Pattern?  
**Answer:** Compound components are a pattern where multiple components work together as one unit and share implicit state, usually through context. A common example is a custom Tabs component with `Tabs`, `TabList`, and `TabPanel`.  
  
### 29. Controlled vs Uncontrolled Components?  
**Answer:** Controlled components are form elements whose value is controlled by React state. Uncontrolled components manage their own value internally in the DOM, and we usually access them with refs. Controlled components are preferred when we need validation, dynamic updates, or predictable form behavior.  
  
### 30. Smart vs Dumb Components?
**Answer:** Smart components handle logic, state, and data fetching, while dumb or presentational components focus only on rendering UI based on props. In modern React, this separation still exists conceptually, although hooks allow both patterns more flexibly.

### Q: How to pass data between functional components in React?
**Answer:** Data flows from parent to child via props. For child-to-parent communication, pass callback functions as props.

```jsx
// Parent to Child (props)
function Parent() {
  const message = "Hello from parent";
  return <Child message={message} />;
}

function Child({ message }) {
  return <p>{message}</p>;
}

// Child to Parent (callback)
function Parent() {
  const [data, setData] = useState('');
  return <Child onData={setData} />;
}

function Child({ onData }) {
  return <button onClick={() => onData('Hello from child')}>Send</button>;
}
```

### Q: What is Prop Drilling in React?
**Answer:** Prop drilling occurs when you pass props through multiple intermediate components that don't need the data, just to deliver it to a deeply nested child. This makes code harder to maintain and refactor.

```jsx
// Prop drilling example
function App() {
  const [user, setUser] = useState({ name: 'Alice' });
  return <Layout user={user} />;           // Layout doesn't use user
}

function Layout({ user }) {
  return <Sidebar user={user} />;          // Sidebar doesn't use user
}

function Sidebar({ user }) {
  return <UserProfile user={user} />;      // UserProfile uses user
}
```

### Q: Why to Avoid Prop Drilling? In how many ways can you avoid Prop Drilling?
**Answer:** Prop drilling creates tight coupling, makes refactoring difficult, and adds unnecessary props to intermediate components.

**Solutions:**
1. **Context API** — Share data without passing through every level
2. **Zustand/Redux** — Global state management
3. **Component Composition** — Pass children as props
4. **Custom Hooks** — Encapsulate shared logic

```jsx
// Context solution
const UserContext = createContext();

function App() {
  const [user, setUser] = useState({ name: 'Alice' });
  return (
    <UserContext.Provider value={user}>
      <Layout />
    </UserContext.Provider>
  );
}

function UserProfile() {
  const user = useContext(UserContext); // Direct access
  return <p>{user.name}</p>;
}
```

### Q: What are Class Components in React?
**Answer:** Class components are ES6 classes that extend `React.Component`. They use `this.state` for state, `this.setState()` to update, and lifecycle methods. Functional components with hooks are now preferred.

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>{this.state.count}</p>
        <button onClick={this.increment}>+</button>
      </div>
    );
  }
}
```

### Q: How to pass data between class components in React?
**Answer:**
```jsx
// Parent to Child — props
class Parent extends React.Component {
  state = { message: 'Hello' };

  render() {
    return <Child message={this.state.message} />;
  }
}

// Child to Parent — callback
class Child extends React.Component {
  render() {
    return (
      <button onClick={() => this.props.onSend('Data from child')}>
        Send
      </button>
    );
  }
}

class Parent extends React.Component {
  handleData = (data) => console.log(data);

  render() {
    return <Child onSend={this.handleData} />;
  }
}
```

### Q: What is the role of `this` keyword in class components?
**Answer:** `this` refers to the component instance. It accesses `this.state`, `this.props`, and `this.setState()`. Arrow functions in class properties automatically bind `this`, avoiding manual binding in constructor.

```jsx
class Button extends React.Component {
  state = { clicked: false };

  // Arrow function — auto-binds this
  handleClick = () => {
    this.setState({ clicked: true }); // this works
  };

  // Regular function — needs binding
  handleClick() {
    this.setState({ clicked: true }); // this is undefined without bind
  }

  render() {
    return <button onClick={this.handleClick}>Click</button>;
  }
}
```

### Q: What are the 5 differences between Functional components & Class components?
**Answer:**

| Feature | Functional Component | Class Component |
|---------|---------------------|-----------------|
| Syntax | JavaScript function | ES6 class extending React.Component |
| State | `useState` hook | `this.state` object |
| Lifecycle | `useEffect` hook | Lifecycle methods (componentDidMount, etc.) |
| `this` keyword | Not used | Required for state/props |
| Performance | Slightly faster | Slightly slower |

---
  
## Props  
  
### 31. What are Props?  
**Answer:** Props are inputs passed from a parent component to a child component. They allow components to receive data and configuration from outside.  
  
### 32. Are props immutable?  
**Answer:** Yes, props are read-only in the child component. A component should never modify its own props. If data needs to change, that change should happen in the parent and be passed down again.  
  
### 33. Props vs State?  
**Answer:** Props come from the parent and are read-only for the child. State is managed inside the component and can change over time. Props are external input, while state is internal mutable data.  
  
### 34. Default Props?  
**Answer:** Default props are fallback values used when a parent does not provide a prop. In modern React with functional components, we often use default parameters instead of `defaultProps` for simple cases.  
  
### 35. Prop Drilling?  
**Answer:** Prop drilling happens when we pass props through multiple intermediate components just to deliver data to a deeply nested child. This can make the code harder to maintain.  
  
### 36. How do you avoid Prop Drilling?  
**Answer:** We can avoid prop drilling by using Context API, global state management like Redux or Zustand, or by restructuring components so data is kept closer to where it is needed.  
  
### 37. Passing functions as props?  
**Answer:** Passing functions as props is a common pattern in React. It allows child components to communicate with parents, for example when a child triggers a parent state update through a callback.  
  
### 38. Children Prop?  
**Answer:** `children` is a special prop in React that represents whatever is placed between a component’s opening and closing tags. It is useful for wrapper components, layouts, and composition patterns.  
  
### 39. React.cloneElement()?  
**Answer:** `React.cloneElement()` is used to clone an existing React element and override or add props to it. It is useful in advanced composition patterns, though it should be used carefully because it can make data flow less obvious.  
  
### 40. React.Children API?  
**Answer:** `React.Children` provides utility methods to safely work with `children`, such as counting, mapping, or converting them into an array. It is useful because `children` is not always a normal array.  
  
---  
  
## State  
  
### 41. What is State?  
**Answer:** State is data managed inside a component that can change over time and trigger re-renders when updated.  
  
### 42. Why use State?  
**Answer:** We use state when the UI needs to react to user interaction, API responses, timers, or any dynamic value that changes during the component’s lifecycle.  
  
### 43. State vs Props?  
**Answer:** Props are passed into a component from outside and are read-only. State belongs to the component and can be updated internally.  
  
### 44. State batching?  
**Answer:** State batching means React groups multiple state updates together and performs a single re-render for better performance. This reduces unnecessary rendering work.  
  
### 45. Why state updates are asynchronous?  
**Answer:** State updates are asynchronous because React schedules them for efficiency and batching. React does not immediately mutate state and re-render on every call because that would be expensive and harder to optimize.  
  
### 46. Immutable State?  
**Answer:** Immutable state means we do not modify the existing state object or array directly. Instead, we create a new copy with the updated values. This helps React detect changes correctly and keeps updates predictable.  
  
### 47. Functional state update?  
**Answer:** A functional state update means passing a function to the setter, like `setCount(prev => prev + 1)`. It is the correct approach when the new state depends on the previous state.  
  
### 48. Lifting State Up?  
**Answer:** Lifting state up means moving shared state to the nearest common parent so multiple child components can access and update the same source of truth.  
  
### 49. Shared State?  
**Answer:** Shared state is state used by more than one component. In React, we usually manage it in the closest common parent, context, or a global store.  
  
### 50. Derived State?  
**Answer:** Derived state is state that can be computed from props or other state values. In most cases, we should avoid storing derived state separately and instead calculate it during render to avoid duplication and inconsistency.  
  
---  
  
## Hooks  
  
### 51. What are Hooks?  
**Answer:** Hooks are functions introduced in React that let functional components use state, lifecycle features, context, refs, and other React capabilities without classes.  
  
### 52. Rules of Hooks?  
**Answer:** Hooks must only be called at the top level of a React function component or custom hook, and never inside loops, conditions, or nested functions. Also, hooks should only be called from React components or custom hooks.  
  
### 53. useState()  
**Answer:** `useState` is used to add local state to a functional component. It returns the current state value and a setter function that schedules an update and re-render.  
  
### 54. useEffect()  
**Answer:** `useEffect` is used to handle side effects like API calls, subscriptions, timers, or manual DOM interactions after render.  
  
### 55. useContext()  
**Answer:** `useContext` allows a component to read context values directly without using a Consumer wrapper. It is useful for sharing data like themes, auth state, or language across the tree.  
  
### 56. useReducer()  
**Answer:** `useReducer` is an alternative to `useState` for managing more complex state logic. It uses a reducer function and dispatch pattern, which is helpful when multiple state transitions are related.  
  
### 57. useMemo()  
**Answer:** `useMemo` memoizes the result of an expensive computation so it only recalculates when dependencies change. It is a performance optimization, not something to use everywhere.  
  
### 58. useCallback()  
**Answer:** `useCallback` memoizes a function reference so that the same function instance is reused unless dependencies change. It is useful when passing callbacks to memoized child components.  
  
### 59. useRef()  
**Answer:** `useRef` gives us a mutable object whose `.current` value persists across renders without causing a re-render when updated. It is used for DOM references or storing mutable values.  
  
### 60. useLayoutEffect()  
**Answer:** `useLayoutEffect` is similar to `useEffect`, but it runs synchronously after DOM mutations and before the browser paints. It is used when we need to measure or adjust layout before the screen updates.  
  
### 61. useImperativeHandle()  
**Answer:** `useImperativeHandle` is used with `forwardRef` to customize the value exposed to the parent through a ref. It allows a child to expose only selected methods instead of its entire internal DOM node.  
  
### 62. useDebugValue()  
**Answer:** `useDebugValue` is mainly used inside custom hooks to display helpful labels or debug information in React DevTools.  
  
### 63. useId()  
**Answer:** `useId` generates stable unique IDs for accessibility-related attributes like `id`, `htmlFor`, and ARIA relationships. It helps avoid ID mismatches, especially with server rendering.  
  
### 64. Custom Hooks?  
**Answer:** Custom hooks are reusable functions that encapsulate stateful logic using built-in hooks. They help us share behavior without repeating code across components.  
  
### 65. When should you create a custom hook?  
**Answer:** I create a custom hook when the same stateful logic or side-effect pattern appears in multiple places, such as form handling, API fetching, debouncing, or subscription logic.  
  
---  
  
## useEffect  
  
### 66. Why useEffect?  
**Answer:** `useEffect` is used to handle side effects that should happen after rendering, such as data fetching, event listeners, subscriptions, timers, or synchronizing external systems with component state.  
  
### 67. Lifecycle of useEffect?  
**Answer:** `useEffect` runs after the component renders. On subsequent renders, if dependencies change, React first runs the cleanup from the previous effect and then runs the new effect. On unmount, the cleanup runs one final time.  
  
### 68. Dependency Array?  
**Answer:** The dependency array tells React when the effect should re-run. If any dependency value changes compared to the previous render, React runs the effect again.  
  
### 69. Empty dependency array?  
**Answer:** An empty dependency array means the effect runs once after the initial render and the cleanup runs on unmount. It behaves similarly to `componentDidMount` plus cleanup on unmount.  
  
### 70. Missing dependency array?  
**Answer:** If there is no dependency array, the effect runs after every render. That is fine in some cases, but often it causes unnecessary work or accidental loops.  
  
### 71. Infinite loops?  
**Answer:** Infinite loops in `useEffect` usually happen when the effect updates state and that state change causes the effect to run again continuously. The fix is to manage dependencies correctly and avoid unnecessary state updates inside the effect.  
  
### 72. Cleanup function?  
**Answer:** The cleanup function is returned from `useEffect` and is used to remove subscriptions, clear timers, cancel requests, or clean external side effects before the effect runs again or the component unmounts.  
  
### 73. API calls inside useEffect?  
**Answer:** API calls are commonly done inside `useEffect` when data should be fetched after render. We should also handle loading, error state, cleanup or cancellation, and dependency management carefully.  
  
### 74. Multiple useEffects?  
**Answer:** Yes, using multiple `useEffect` calls is actually a good practice when the side effects are unrelated. It keeps logic separated and easier to understand.  
  
### 75. Common mistakes in useEffect?  
**Answer:** Common mistakes include missing dependencies, adding unstable dependencies unnecessarily, causing infinite loops, forgetting cleanup, storing derived data in state unnecessarily, and using `useEffect` for logic that should happen directly during render.  
  
---  
  
## Rendering  
  
### 76. What causes re-render?  
**Answer:** A component re-renders when its state changes, its props change, its parent re-renders, or the context value it consumes changes.  
  
### 77. Parent re-render effect?  
**Answer:** When a parent re-renders, React also re-renders its children by default, even if the child props did not change, unless optimizations like `React.memo` are used.  
  
### 78. Child re-render?  
**Answer:** A child re-renders when its parent re-renders, when its own state changes, when its props change, or when the context it uses changes.  
  
### 79. Prevent unnecessary renders?  
**Answer:** I prevent unnecessary renders by keeping state local when possible, using `React.memo` for pure components, memoizing expensive values with `useMemo`, memoizing callbacks with `useCallback`, and avoiding unnecessary prop changes.  
  
### 80. React.memo?  
**Answer:** `React.memo` is a higher-order component that memoizes a functional component and skips re-rendering if its props are shallowly equal to the previous ones.  
  
### 81. useMemo?  
**Answer:** `useMemo` memoizes a computed value. I use it when a calculation is expensive or when I need referential stability for objects or arrays passed to child components.  
  
### 82. useCallback?  
**Answer:** `useCallback` memoizes a function reference. I mainly use it when passing callbacks to memoized children or when a hook dependency requires a stable function identity.  
  
### 83. Lazy Loading?  
**Answer:** Lazy loading means loading a component or resource only when it is needed instead of loading everything upfront. In React, this improves initial bundle size and load performance.  
  
### 84. Code Splitting?  
**Answer:** Code splitting means breaking the JavaScript bundle into smaller chunks so only the required code is loaded at a given time. This reduces initial load cost.  
  
### 85. Suspense?  
**Answer:** Suspense is a React feature that lets us define a fallback UI while waiting for a lazy-loaded component or certain async resources to be ready.  
  
---  
  
## Virtual DOM  
  
### 86. What is Virtual DOM?  
**Answer:** The Virtual DOM is a lightweight JavaScript representation of the real DOM. React uses it to compare UI changes efficiently before updating the browser DOM.  
  
### 87. Virtual DOM vs Real DOM?  
**Answer:** The real DOM is the actual browser structure and updates to it can be expensive. The Virtual DOM is an in-memory representation that React compares first so it can make only the minimal necessary real DOM updates.  
  
### 88. Diffing Algorithm?  
**Answer:** React’s diffing algorithm compares the previous and next Virtual DOM trees and determines what changed. It uses heuristics to do this efficiently instead of comparing everything deeply in a slow way.  
  
### 89. Reconciliation?  
**Answer:** Reconciliation is the process React uses to compare two Virtual DOM trees and update the real DOM with the smallest possible set of changes.  
  
### 90. Why is Virtual DOM faster?  
**Answer:** It is not that Virtual DOM itself is magically faster than the real DOM in all situations. The main benefit is that React avoids unnecessary direct DOM operations by batching and applying only the minimal required updates.  
  
### 91. Keys in React?  
**Answer:** Keys help React identify list items across renders so it can track which items were added, removed, or reordered. Stable keys improve correctness and performance during reconciliation.  
  
### 92. Why shouldn't index be used as key?  
**Answer:** Using index as a key can cause issues when list items are inserted, deleted, or reordered because React may incorrectly associate old state with the wrong item. It is safe only for static lists that never change order.  
  
---  
  
## Forms  
  
### 93. Controlled Components?  
**Answer:** Controlled components are form inputs whose value is fully controlled by React state. The displayed value comes from state, and every change updates state through an event handler.  
  
### 94. Uncontrolled Components?  
**Answer:** Uncontrolled components store form values in the DOM itself instead of React state. We usually access their value through refs. They are simpler in some cases, but give less control.  
  
### 95. Form validation?  
**Answer:** Form validation can be done using controlled state, schema validation libraries like Yup or Zod, or form libraries. In React, I usually validate on change, blur, or submit depending on UX needs.  
  
### 96. React Hook Form?  
**Answer:** React Hook Form is a popular library for form handling that focuses on performance and minimal re-renders. It works well with uncontrolled inputs and provides validation, field arrays, and good developer ergonomics.  
  
### 97. Formik?  
**Answer:** Formik is a form library that simplifies form state, validation, and submission. It is easy to use, though compared to React Hook Form it may cause more re-renders in larger forms.  
  
### 98. Handling file uploads?  
**Answer:** File uploads are usually handled using an input of type file, reading the selected file from `event.target.files`, and sending it with `FormData` to the backend. We may also add validation, preview, and progress tracking.  
  
### 99. Handling multiple inputs?  
**Answer:** For multiple inputs, I typically keep form state as an object and update fields dynamically using the input `name` attribute and a shared change handler.  
  
### 100. Dynamic forms?  
**Answer:** Dynamic forms are forms where fields are added, removed, or configured at runtime. I usually manage them using arrays in state or form libraries that support field arrays well.  
  
---  
  
## Events  
  
### 101. Synthetic Events?  
**Answer:** Synthetic Events are React’s cross-browser wrapper around native browser events. They provide a consistent API so event handling works similarly across browsers.  
  
### 102. Event Bubbling?  
**Answer:** Event bubbling means an event starts at the target element and then propagates upward through its parent elements.  
  
### 103. Event Capturing?  
**Answer:** Event capturing is the opposite phase where the event travels from the root down to the target before bubbling back up.  
  
### 104. preventDefault()?  
**Answer:** `preventDefault()` stops the browser’s default action for an event, for example preventing form submission reload or stopping a link from navigating.  
  
### 105. stopPropagation()?  
**Answer:** `stopPropagation()` prevents the event from continuing to propagate to parent elements.  
  
### 106. Event Delegation?  
**Answer:** Event delegation is a pattern where a parent handles events for its children instead of attaching listeners to every child individually. React internally uses event delegation efficiently for many events.  
  
---  
  
## Context API  
  
### 107. What is Context API?  
**Answer:** Context API is React’s built-in way to share values like theme, auth, or configuration across the component tree without passing props manually through every level.  
  
### 108. Why Context API?  
**Answer:** We use Context API to avoid prop drilling and make globally relevant values accessible to deeply nested components.  
  
### 109. Context vs Redux?  
**Answer:** Context is good for sharing relatively simple global values. Redux is more suitable when the application has complex global state logic, advanced debugging needs, middleware, or predictable centralized state transitions.  
  
### 110. Multiple Contexts?  
**Answer:** Yes, React supports multiple contexts. In real applications, it is common to separate concerns like auth context, theme context, and settings context rather than combining everything into one.  
  
### 111. Context performance issues?  
**Answer:** A common issue is that when a context value changes, all consuming components re-render. To reduce this, I split contexts by concern, memoize values, and avoid putting frequently changing data unnecessarily into large shared contexts.  
  
---  
  
## Zustand

### 112. What is Zustand?
**Answer:** Zustand (German for "state") is a small, unopinionated state management library for React. It provides a global store via a hook-based API with minimal boilerplate. It uses `useSyncExternalStore` internally for concurrent-safe reads.

### 113. Why Zustand over Redux?
**Answer:** Zustand is simpler, more lightweight (~1-3KB), and easier to set up. It requires no Provider, no actions/reducers ceremony, and supports selectors for performance. Redux is more structured with richer tooling for large teams.

| Pain Point | Zustand Solution |
|------------|------------------|
| Actions + reducers ceremony | `set()` directly in store |
| Provider required | No Provider needed |
| Boilerplate | Minimal API surface |
| Learning curve | Learn in an afternoon |

### 114. Zustand vs Context API?
**Answer:** Use Zustand when state updates frequently or many components need different slices. Use Context when theme/locale/auth rarely changes or state is scoped to a subtree.

| Feature | Zustand | Context |
|---------|---------|---------|
| Re-renders | Only selected fields | All consumers |
| Built-in selectors | Yes | No |
| Middleware | persist, devtools | None |
| Provider | Not required | Required |

### 115. Store Creation?
**Answer:** Create a store using `create` from zustand. It returns a React hook.

```typescript
import { create } from 'zustand';

interface CounterState {
  count: number;
  increment: () => void;
  decrement: () => void;
}

export const useCounterStore = create<CounterState>((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
}));

// In a component
function Counter() {
  const count = useCounterStore((s) => s.count);
  const increment = useCounterStore((s) => s.increment);
  return <button onClick={increment}>{count}</button>;
}
```

### 116. Selectors and Performance?
**Answer:** A selector is a function `(state) => slice` passed to the hook. The component re-renders only when the selected value changes (via `Object.is` comparison).

```typescript
// ✅ Good — subscribe only to `user.name`
const userName = useAuthStore((s) => s.user?.name);

// ❌ Bad — subscribes to entire store; any change re-renders
const store = useAuthStore();
```

### 117. Shallow Comparison?
**Answer:** `shallow` compares first-level keys of two objects with `Object.is`. Used when a selector returns an object/array to prevent unnecessary re-renders.

```typescript
import { useShallow } from 'zustand/react/shallow';

// v5 recommended: useShallow hook
const { user, login } = useAuthStore(
  useShallow((s) => ({ user: s.user, login: s.login }))
);
```

### 118. Middleware?
**Answer:** Middleware wraps the store creator to extend `set`, `get`, or `store`. Applied right-to-left (innermost first).

| Middleware | Purpose |
|------------|---------|
| `persist` | localStorage/sessionStorage sync |
| `devtools` | Redux DevTools extension |
| `immer` | Mutable-style updates |
| `subscribeWithSelector` | Granular `subscribe` |

```typescript
import { create } from 'zustand';
import { devtools, persist } from 'zustand/middleware';

const useStore = create()(
  devtools(
    persist(
      (set) => ({ count: 0 }),
      { name: 'counter-storage' }
    ),
    { name: 'CounterStore' }
  )
);
```

### 119. Persist Middleware?
**Answer:** Saves state to storage (default localStorage), rehydrates on load, supports partial persist, versioning, and migrations.

```typescript
import { persist, createJSONStorage } from 'zustand/middleware';

export const useSettingsStore = create()(
  persist(
    (set) => ({
      theme: 'light',
      setTheme: (theme) => set({ theme }),
    }),
    {
      name: 'app-settings',
      partialize: (state) => ({ theme: state.theme }), // only persist theme
      storage: createJSONStorage(() => localStorage),
    }
  )
);
```

### 120. Async Actions?
**Answer:** Write async functions inside the store — no thunk middleware required.

```typescript
export const useUserStore = create((set, get) => ({
  user: null,
  status: 'idle',
  error: null,

  fetchUser: async (id: string) => {
    set({ status: 'loading', error: null });
    try {
      const user = await api.users.get(id);
      set({ user, status: 'success' });
    } catch (e) {
      set({ status: 'error', error: (e as Error).message });
    }
  },
}));
```

### 121. Subscribe Outside React?
**Answer:** Use `subscribe`, `getState`, and `setState` for non-React consumers (WebSocket handlers, analytics, tests).

```typescript
// Read without subscribing
const token = useAuthStore.getState().token;

// Imperative update outside component
useAuthStore.setState({ token: null });

// Subscribe to changes
const unsub = useAuthStore.subscribe((state) => {
  console.log('State changed', state);
});
unsub(); // cleanup
```

### 122. Best Practices?
**Answer:**
1. **One store per domain** — auth, ui, feature modules
2. **Always use selectors** — `useStore((s) => s.field)`
3. **Actions inside store** — keep components thin
4. **Don't persist secrets** — tokens in memory or httpOnly cookies
5. **Server state in React Query**, client state in Zustand
6. **Name DevTools actions** for traceability

```typescript
// Custom selector hooks
export const useUser = () => useAuthStore((s) => s.user);
export const useLogin = () => useAuthStore((s) => s.login);
```

---
  
## Routing  
  
### 125. React Router?  
**Answer:** React Router is a routing library for React that allows us to map URLs to components in client-side applications.  
  
### 126. BrowserRouter?  
**Answer:** `BrowserRouter` uses the HTML5 history API to keep the UI in sync with the URL and enables clean URLs without hashes.  
  
### 127. Routes?  
**Answer:** `Routes` is the container used in modern React Router to define route matching and render the best matching route element.  
  
### 128. Route Parameters?  
**Answer:** Route parameters are dynamic parts of a URL, like `/users/:id`, which we can access using hooks like `useParams`.  
  
### 129. Nested Routes?  
**Answer:** Nested routes allow one route to render child routes inside it. This is useful for layouts, dashboards, and hierarchical page structures.  
  
### 130. Protected Routes?  
**Answer:** Protected routes are routes that only authenticated or authorized users can access. Usually we wrap the route element in logic that checks auth state and redirects if needed.  
  
### 131. Navigate?  
**Answer:** `Navigate` is used for declarative redirection in React Router, for example redirecting unauthenticated users to a login page.  
  
### 132. Outlet?  
**Answer:** `Outlet` is a placeholder in a parent route component where matched child routes are rendered.  
  
### 133. Lazy Routes?
**Answer:** Lazy routes are routes whose components are loaded only when the user navigates to them. This improves initial bundle performance.

### Q: How to Implement Routing in React?
**Answer:**
```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users/:id" element={<UserProfile />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### Q: What are Route Parameters in React Routing?
**Answer:** Route parameters are dynamic segments in URLs (e.g., `/users/:id`). They're accessed via `useParams` hook.

```jsx
<Route path="/users/:id" element={<UserProfile />} />

function UserProfile() {
  const { id } = useParams();
  return <h1>User {id}</h1>;
}
```

### Q: What is the role of Switch Component in React Routing?
**Answer:** In React Router v6, `Switch` is replaced by `Routes`. It renders the first matching route exclusively. Without it, all matching routes would render simultaneously.

```jsx
// React Router v6
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
</Routes>

// Only one route renders at a time
```

### Q: What is the role of exact prop in React Routing?
**Answer:** In React Router v5, `exact` ensures a route matches the URL exactly. Without it, `/about` would also match `/about/team`. In v6, routes are exact by default (no `exact` prop needed).

```jsx
// React Router v5 — without exact
<Route path="/about" component={About} /> // matches /about/team too

// React Router v5 — with exact
<Route path="/about" exact component={About} /> // matches only /about

// React Router v6 — exact by default
<Route path="/about" element={<About />} />
```

---
  
## API Integration  
  
### 134. Fetch vs Axios?  
**Answer:** `fetch` is a built-in browser API and is lightweight, but it requires more manual handling for JSON conversion and error checking. Axios provides a richer API, interceptors, automatic JSON handling, timeout support, and broader convenience features.  
  
### 135. API Error Handling?  
**Answer:** I handle API errors by checking response status, using `try/catch`, showing meaningful error UI, logging failures when needed, and separating expected business errors from unexpected server or network errors.  
  
### 136. Loading State?  
**Answer:** Loading state tells the UI that an async operation is in progress. It helps improve UX by showing spinners, skeletons, or disabled actions while waiting for data.  
  
### 137. Retry API?  
**Answer:** API retries should be used carefully for transient failures like network issues or temporary server errors. I usually implement retry with limits, delay, and sometimes exponential backoff.  
  
### 138. Cancel API Requests?  
**Answer:** Yes, canceling requests is important when a component unmounts or when a new request makes the old one irrelevant. It avoids race conditions and wasted work.  
  
### 139. AbortController?  
**Answer:** `AbortController` is a browser API used to cancel fetch requests. In React, I often use it inside `useEffect` cleanup to cancel pending requests when the component unmounts or dependencies change.  
  
---  
  
## Performance  
  
### 140. How to optimize React applications?  
**Answer:** I optimize React applications by minimizing unnecessary renders, keeping state close to where it is used, memoizing only where it provides value, lazy loading routes and components, optimizing bundles, virtualizing large lists, caching server state, and measuring performance before making changes.  
  
### 141. Memoization?  
**Answer:** Memoization means caching results or references so they can be reused instead of recreated every render. In React, common memoization tools are `React.memo`, `useMemo`, and `useCallback`.  
  
### 142. Bundle Optimization?  
**Answer:** Bundle optimization includes code splitting, tree shaking, removing dead code, compressing assets, avoiding oversized dependencies, and lazy loading non-critical features.  
  
### 143. Tree Shaking?  
**Answer:** Tree shaking is the process of removing unused exports from the final bundle during build time, especially with ES Modules.  
  
### 144. Dynamic Imports?  
**Answer:** Dynamic imports let us load modules on demand using `import()`. They are commonly used for lazy loading and route-based code splitting.  
  
### 145. Image Optimization?  
**Answer:** Image optimization includes serving appropriately sized images, using modern formats like WebP or AVIF, lazy loading, responsive images, caching, and using optimized components like Next.js Image when applicable.  
  
---  
  
## Project Structure

### Q: What is NPM? What is the role of node_modules folder?
**Answer:** NPM (Node Package Manager) is a package manager for JavaScript. It downloads and manages dependencies for your project. The `node_modules` folder contains all installed packages and their dependencies.

```bash
npm install react react-dom    # Install packages
npm install --save-dev jest    # Dev dependencies
npm run build                 # Run scripts
```

### Q: What is the role of public folder in React?
**Answer:** The `public` folder contains static assets served directly without processing. It includes `index.html` (the entry point), favicon, images, and other files that don't require build processing.

```
public/
├── index.html      # Main HTML template
├── favicon.ico     # Browser tab icon
└── assets/         # Static images, fonts
```

### Q: What is the role of src folder in React?
**Answer:** The `src` folder contains all source code that gets processed by the build tool. Components, styles, tests, utilities, and application logic go here.

```
src/
├── components/     # Reusable UI components
├── pages/          # Route-level components
├── hooks/          # Custom hooks
├── utils/          # Helper functions
├── App.js          # Root component
├── index.js        # Entry point
└── styles/         # CSS/SCSS files
```

### Q: What is the role of index.html page in React?
**Answer:** `index.html` is the single HTML file that loads the React application. It contains a `<div id="root">` where React mounts the entire app. All routing and rendering happens client-side within this single page.

```html
<!DOCTYPE html>
<html>
<head>
  <title>React App</title>
</head>
<body>
  <div id="root"></div>  <!-- React mounts here -->
  <script src="/static/js/bundle.js"></script>
</body>
</html>
```

### Q: What is the role of index.js file and ReactDOM in React?
**Answer:** `index.js` is the JavaScript entry point. It uses `ReactDOM.createRoot()` to render the root component into the `#root` div in `index.html`.

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### Q: What is the role of App.js file in React?
**Answer:** `App.js` is the root component of the application. It contains the main component tree, routing setup, global providers (context, state), and layout structure. All other components are rendered within App.

```jsx
function App() {
  return (
    <AuthProvider>
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/dashboard" element={<Dashboard />} />
        </Routes>
      </BrowserRouter>
    </AuthProvider>
  );
}
export default App;
```

### Q: What is the role of function and return inside App.js?
**Answer:** The function defines the component logic and the return statement contains the JSX that React renders. The return must have a single root element (or Fragment).

```jsx
function App() {
  // Logic, hooks, state here
  
  return (        // What gets rendered to the DOM
    <div>
      <Header />
      <main>{children}</main>
      <Footer />
    </div>
  );
}
```

### Q: Can we have a function without a return inside App.js?
**Answer:** No. A React component must return JSX (or null). Without a return, React cannot determine what to render. If you return nothing, return `null` explicitly.

```jsx
// ❌ Invalid — no return
function App() {
  const x = 5;
}

// ✅ Valid — returns null (renders nothing)
function App() {
  return null;
}
```

### Q: What is the role of export default inside App.js?
**Answer:** `export default` allows other files to import the component. It's the main export of the file. You can have only one default export per file.

```jsx
// App.js
function App() {
  return <div>Hello</div>;
}
export default App;  // Named export

// index.js
import App from './App';  // Import default export
```

### Q: Does the file name and component name must be same in React?
**Answer:** No, it's not required but it's a strong convention. The file name can be anything, but the component name must match what you use in JSX. Convention is PascalCase for both file and component names for clarity.

```jsx
// File: UserProfile.js (optional naming)
function UserCard() {  // Component can have different name
  return <div>Profile</div>;
}
export default UserCard;

// Imported as
import UserCard from './UserProfile';  // Works fine
```

---

## React Hooks Deep Dive

### Q: What are the Top React Hooks?
**Answer:**
| Hook | Purpose |
|------|---------|
| `useState` | Local state management |
| `useEffect` | Side effects, lifecycle |
| `useContext` | Consume context |
| `useReducer` | Complex state logic |
| `useMemo` | Memoize expensive computations |
| `useCallback` | Memoize functions |
| `useRef` | Mutable references |
| `useLayoutEffect` | Synchronous side effects |
| `useId` | Unique IDs for accessibility |

### Q: What is the role of useState() hook and how it works?
**Answer:** `useState` adds local state to functional components. It returns `[state, setState]`. Calling `setState` triggers a re-render.

```jsx
const [count, setCount] = useState(0);

// State update
setCount(count + 1);                    // Direct value
setCount(prev => prev + 1);            // Functional update (preferred)

// Object state
const [user, setUser] = useState({ name: '', age: 0 });
setUser({ ...user, name: 'Alice' });   // Must spread to preserve
```

### Q: What is the role of useEffect()? How it works and what is its use?
**Answer:** `useEffect` handles side effects: API calls, subscriptions, timers, DOM manipulation. It runs after render.

```jsx
useEffect(() => {
  // Side effect here
  const data = await fetch('/api');
  
  return () => {
    // Cleanup (optional)
    // Runs before next effect or unmount
  };
}, []);  // Dependency array
```

### Q: What is Dependency Array in useEffect() hook?
**Answer:** The dependency array tells React when to re-run the effect. If any dependency changes, the effect runs again.

```jsx
// Runs on every render
useEffect(() => {
  console.log('Always runs');
});

// Runs once on mount
useEffect(() => {
  console.log('Mount only');
}, []);

// Runs when userId changes
useEffect(() => {
  fetchUser(userId);
}, [userId]);
```

### Q: What is the meaning of the empty array [] in the useEffect()?
**Answer:** An empty dependency array `[]` means the effect has no dependencies, so it runs only once after the initial render (mount) and cleans up on unmount. It's equivalent to `componentDidMount` + cleanup.

```jsx
useEffect(() => {
  console.log('Runs once on mount');
  
  return () => {
    console.log('Cleanup on unmount');
  };
}, []);  // Empty array
```

---

## Context API (Advanced)

### Q: What is the role of useContext() hook?
**Answer:** `useContext` consumes context values without requiring a Consumer wrapper. It provides cleaner syntax than the Consumer component.

```jsx
const ThemeContext = createContext('light');

// Provider
<ThemeContext.Provider value="dark">
  <App />
</ThemeContext.Provider>

// Consumer
function Button() {
  const theme = useContext(ThemeContext);
  return <button className={theme}>Click</button>;
}
```

### Q: What is createContext() method? What are Provider & Consumer properties?
**Answer:** `createContext` creates a context object with `Provider` and `Consumer` components. Provider provides values to descendants. Consumer subscribes to those values.

```jsx
const AuthContext = createContext(null);

// Provider — provides value
function App() {
  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      <Child />
    </AuthContext.Provider>
  );
}

// Consumer — subscribes to value
function Child() {
  return (
    <AuthContext.Consumer>
      {({ user }) => <p>{user?.name}</p>}
    </AuthContext.Consumer>
  );
}
```

### Q: When to use useContext() hook instead of props in real applications?
**Answer:** Use `useContext` when:
- Theme, locale, auth state shared across many components
- Avoiding prop drilling through 3+ levels
- App-wide settings that rarely change
- You want zero additional dependencies (vs Zustand/Redux)

### Q: What is useReducer() hook? When to use useState() and when useReducer()?
**Answer:** `useReducer` manages complex state logic with a reducer function and dispatch. Use it when state transitions are complex or related.

```jsx
const [state, dispatch] = useReducer(reducer, initialState);

function reducer(state, action) {
  switch (action.type) {
    case 'increment': return { count: state.count + 1 };
    case 'decrement': return { count: state.count - 1 };
    default: throw new Error();
  }
}

// Use useState for simple state
const [count, setCount] = useState(0);

// UseReducer for complex state
const [state, dispatch] = useReducer(reducer, { count: 0, items: [] });
```

### Q: What are the differences between useState() and useReducer() Hook?
**Answer:**

| Feature | useState | useReducer |
|---------|----------|------------|
| Complexity | Simple state | Complex state logic |
| Updates | `setState(value)` | `dispatch({ type, payload }) |
| Logic location | Inline | Reducer function (separate) |
| Debugging | Harder | Easier with action logs |
| Testing | Component needed | Pure function testable |

### Q: What are dispatch & reducer function in useReducer Hook?
**Answer:**
- **dispatch** sends actions to the reducer (like `setState` but with action types)
- **reducer** is a pure function that takes `(state, action)` and returns new state

```jsx
function reducer(state, action) {
  switch (action.type) {
    case 'add':
      return { ...state, items: [...state.items, action.payload] };
    case 'remove':
      return { ...state, items: state.items.filter(i => i.id !== action.id) };
    default:
      return state;
  }
}

// In component
dispatch({ type: 'add', payload: newItem });
dispatch({ type: 'remove', id: 5 });
```

### Q: What is the purpose of passing initial state as an object in useReducer?
**Answer:** Using an object groups related state fields, making updates atomic and state structure clear. It prevents missing fields and makes the reducer easier to maintain.

```jsx
// ✅ Object state — clear structure
const initialState = { count: 0, items: [], loading: false };

// ❌ Individual states — harder to manage
const [count, setCount] = useState(0);
const [items, setItems] = useState([]);
const [loading, setLoading] = useState(false);
```

---

## Component Lifecycle

### Q: What are Component Lifecycle Phases?
**Answer:** Three phases in class components:
1. **Mounting** — Component is created and inserted into DOM
2. **Updating** — Component re-renders due to props/state changes
3. **Unmounting** — Component is removed from DOM

```
Mounting: constructor → getDerivedStateFromProps → render → componentDidMount
Updating: getDerivedStateFromProps → shouldComponentUpdate → render → getSnapshotBeforeUpdate → componentDidUpdate
Unmounting: componentWillUnmount
```

### Q: What are Component Lifecycle Methods?
**Answer:**
| Phase | Method | Purpose |
|-------|--------|---------|
| Mount | `componentDidMount` | API calls, subscriptions |
| Mount | `componentWillMount` | Deprecated |
| Update | `componentDidUpdate` | After re-render |
| Update | `shouldComponentUpdate` | Performance optimization |
| Unmount | `componentWillUnmount` | Cleanup (cancel, unsubscribe) |

### Q: What is the role of super keyword in constructor?
**Answer:** `super` calls the parent class (`React.Component`) constructor. It must be called before accessing `this`. Without it, `this` is undefined.

```jsx
class Button extends React.Component {
  constructor(props) {
    super(props);  // Required — calls React.Component constructor
    this.state = { clicked: false };
  }
}
```

### Q: What is the role of render() method in component life cycle?
**Answer:** `render()` is required in class components. It's called on every update and returns JSX. It should be pure — no side effects, just UI description based on props/state.

```jsx
class Counter extends React.Component {
  render() {
    return <p>{this.props.count}</p>;
  }
}
```

### Q: How can State be maintained in a class component?
**Answer:** Initialize in constructor or class field. Use `this.setState()` to update (never modify `this.state` directly).

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  increment = () => {
    this.setState({ count: this.state.count + 1 });
    // Or functional form
    this.setState(prev => ({ count: prev.count + 1 }));
  };

  render() {
    return <button onClick={this.increment}>{this.state.count}</button>;
  }
}
```

### Q: What is the role of componentDidMount() method?
**Answer:** Runs after component mounts (inserted into DOM). Use for API calls, subscriptions, timers, or any setup requiring DOM access.

```jsx
componentDidMount() {
  // API call
  fetch('/api/data')
    .then(res => res.json())
    .then(data => this.setState({ data }));
  
  // Subscription
  window.addEventListener('resize', this.handleResize);
}

componentWillUnmount() {
  window.removeEventListener('resize', this.handleResize);
}
```

---

## Forms (Extended)

### Q: What are Controlled Components in React?
**Answer:** Controlled components are form elements where React state is the single source of truth. The input value comes from state, and every change updates state via event handlers.

```jsx
function Form() {
  const [name, setName] = useState('');
  
  return (
    <input 
      value={name} 
      onChange={(e) => setName(e.target.value)} 
    />
  );
}
```

### Q: What are the Differences between Controlled & Uncontrolled Components?
**Answer:**

| Feature | Controlled | Uncontrolled |
|---------|------------|--------------|
| Data source | React state | DOM |
| Value access | `state.value` | `ref.current.value` |
| Instant validation | Yes | No |
| Dynamic input | Easy | Harder |
| Code complexity | More | Less |
| Use case | Forms, validation | Simple inputs, file uploads |

### Q: How to handle multiple input fields in a controlled form?
**Answer:** Use a single state object with the input's `name` attribute as the key.

```jsx
function Form() {
  const [form, setForm] = useState({ name: '', email: '' });
  
  const handleChange = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };
  
  return (
    <form>
      <input name="name" value={form.name} onChange={handleChange} />
      <input name="email" value={form.email} onChange={handleChange} />
    </form>
  );
}
```

### Q: How do you handle form validation in a controlled component?
**Answer:**
```jsx
function Form() {
  const [email, setEmail] = useState('');
  const [error, setError] = useState('');
  
  const validate = (value) => {
    if (!value) return 'Email is required';
    if (!/\S+@\S+\.\S+/.test(value)) return 'Invalid email';
    return '';
  };
  
  const handleChange = (e) => {
    const value = e.target.value;
    setEmail(value);
    setError(validate(value));
  };
  
  return (
    <div>
      <input value={email} onChange={handleChange} />
      {error && <span>{error}</span>}
    </div>
  );
}
```

### Q: In what scenarios might using uncontrolled components be advantageous?
**Answer:**
- File inputs (no controlled value possible)
- Integration with non-React code
- Quick prototypes
- Forms with many fields (less re-renders)
- Initial values only (not dynamic updates)

---

## Advanced React

### Q: What is Code Splitting in React?
**Answer:** Code splitting breaks your bundle into smaller chunks loaded on demand. It reduces initial load time by only loading code needed for the current view.

### Q: What is the role of Lazy and Suspense methods in React?
**Answer:** `lazy` dynamically imports components. `Suspense` shows a fallback while loading.

```jsx
import { lazy, Suspense } from 'react';

const Dashboard = lazy(() => import('./Dashboard'));
const Settings = lazy(() => import('./Settings'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/settings" element={<Settings />} />
      </Routes>
    </Suspense>
  );
}
```

### Q: What are the Pros and Cons of Code Splitting?
**Answer:**

| Pros | Cons |
|------|------|
| Faster initial load | Loading states/fallback UI |
| Smaller bundles | Network requests for chunks |
| Better caching | Complexity in setup |
| Improved performance | Potential layout shifts |

### Q: What is the role of the import() function in code splitting?
**Answer:** `import()` is a dynamic import that returns a Promise. It tells the bundler to create a separate chunk for the imported module, loaded only when called.

```jsx
// Static import — included in bundle
import Button from './Button';

// Dynamic import — separate chunk
const Button = lazy(() => import('./Button'));

// Conditional dynamic import
const loadAdmin = () => import('./AdminPanel');
```

### Q: What is the purpose of the fallback prop in Suspense?
**Answer:** `fallback` is the UI shown while lazy components load. It must be a valid React element (not a string).

```jsx
<Suspense fallback={<LoadingSpinner />}>
  <LazyComponent />
</Suspense>

// Multiple fallbacks for nested lazy components
<Suspense fallback={<PageLoader />}>
  <Header />
  <Suspense fallback={<ContentLoader />}>
    <LazyContent />
  </Suspense>
</Suspense>
```

### Q: Can you dynamically load CSS files using code splitting in React?
**Answer:** Yes, using dynamic `import()` or build tool features. CSS-in-JS libraries handle this automatically. For plain CSS, you can use `style-loader` or extract CSS plugins.

```jsx
// Dynamic CSS import
const loadStyles = async () => {
  await import('./styles/dark-theme.css');
};

// CSS-in-JS (automatic code splitting)
const StyledDiv = styled.div`
  color: ${props => props.theme.primary};
`;
```

### Q: How do you inspect and analyze the generated chunks in a React application?
**Answer:**
```bash
# Build with source maps
npm run build

# Analyze bundle
npx source-map-explorer build/static/js/*.js

# Or use webpack-bundle-analyzer
npm install --save-dev webpack-bundle-analyzer
```

```js
// webpack.config.js
const { BundleAnalyzerPlugin } = require('webpack-bundle-analyzer');

module.exports = {
  plugins: [new BundleAnalyzerPlugin()]
};
```

```bash
# Check bundle size
npm run build
du -sh build/static/js/
ls -lh build/static/js/
```

---  
  
### 146. Error Boundaries?  
**Answer:** Error boundaries are React components that catch JavaScript errors in their child component tree during rendering, lifecycle methods, and constructors. They prevent the entire app from crashing and allow fallback UI. Traditionally, they are implemented with class components.  
  
### 147. Portals?  
**Answer:** Portals allow us to render a child component into a different part of the DOM tree while keeping it logically inside the React tree. They are commonly used for modals, tooltips, and overlays.  
  
### 148. ForwardRef?  
**Answer:** `forwardRef` allows a parent component to pass a ref through a component to one of its child DOM nodes or exposed instances. It is useful when building reusable input or UI wrapper components.  
  
### 149. Strict Mode?  
**Answer:** Strict Mode is a development-only tool that helps identify unsafe patterns, side effects, and deprecated usage. It intentionally re-runs some logic in development to surface problems early.  
  
### 150. Concurrent Rendering?  
**Answer:** Concurrent Rendering is React’s ability to prepare multiple UI states and prioritize updates more intelligently so the app stays responsive. It does not mean