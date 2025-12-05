# ⚛️ **How React.js Works (Easy Explanation)**

React.js is a **JavaScript library for building UI**.
It works using:

* **Components**
* **Virtual DOM**
* **Reconciliation**
* **Hooks**

Let’s break it down.

---

# 🧠 1. **React = Component-Based Architecture**

Everything in React is a **component**:

* Navbar
* Button
* Sidebar
* Product card

Example:

```jsx
function Button() {
  return <button>Click</button>;
}
```

### Components return UI (JSX)

React builds the UI by combining components like Lego blocks.

---

# ⚡ 2. **React Uses Virtual DOM**

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20241212235246933476/Browser-DOM-Virtual-DOM.webp?utm_source=chatgpt.com)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2ANLNoFfBWzu8Uu1RgWw3Z9g.jpeg?utm_source=chatgpt.com)

![Image](https://media2.dev.to/dynamic/image/width%3D1280%2Cheight%3D720%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fxjqsuome198owgamcgr3.jpeg?utm_source=chatgpt.com)

### Real DOM = Slow

Because changing HTML directly is expensive.

### Virtual DOM = Fast

React creates a **lightweight copy** of the real DOM in memory.

Process:

1. You update state
2. React creates a **new virtual DOM**
3. React compares new vs old (diff algorithm)
4. React updates **only changed parts** of the real DOM

This process is called **Reconciliation**.

---

# 🔁 3. **How React Updates UI (State → Rerender)**

### Example:

```jsx
const [count, setCount] = useState(0);

<button onClick={() => setCount(count + 1)}>Add</button>
```

Flow:

```
setCount() → state changes → component re-renders → 
React updates only the changed UI part
```

React does NOT reload the full page.

---

# 🔨 4. **React Components Rendering Process**

![Image](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/ogimage.png?utm_source=chatgpt.com)

![Image](https://reactnative.dev/assets/images/render-pipeline-3-db2c1aa465ae7d76346b879966938b3d.png?utm_source=chatgpt.com)

### Step-by-step:

1. Component function runs
2. JSX is converted to Virtual DOM
3. Diff algorithm runs
4. Only changed nodes update on the real DOM
5. Browser paints the new UI

---

# 🧵 5. **One-Way Data Flow**

React uses **unidirectional data flow**:

```
Parent → Child
```

Example:

```jsx
<Child name="Sangram" />
```

Child receives `name` as props.

---

# 🪝 6. **Hooks Control Everything**

Hooks give React power:

| Hook          | Purpose                    |
| ------------- | -------------------------- |
| `useState`    | Manage state               |
| `useEffect`   | Handle side effects        |
| `useContext`  | Global data                |
| `useRef`      | Access DOM or store values |
| `useMemo`     | Optimization               |
| `useCallback` | Prevent re-renders         |

### Example (useEffect):

```js
useEffect(() => {
  console.log("Component Mounted");
}, []);
```

---

# 🎯 7. **How React Works Internally (Deep Flow)**

![Image](https://www.innovationm.com/blog/wp-content/uploads/2019/11/Fibre-architecture-624x347.png?utm_source=chatgpt.com)

![Image](https://cdn.prod.website-files.com/5d2dd7e1b4a76d8b803ac1aa/5f604fd80b9cb018d27eeda5_UsoMdBUqB9kLNWjrraBggD3QUb-fuTlKw_u6h_vBx5OnMHZnxTYUQcaoZa_nP9fwCA1nWLEvAnAnlwjMDg2io4z7DPJ5LA8K7qSwTs4_rBJHVuZQrEX-TZOzzOPyhN7FEncG91vy.png?utm_source=chatgpt.com)

![Image](https://jser.dev/static/scheduler-1.png?utm_source=chatgpt.com)

React uses **Fiber Architecture** which breaks rendering into small units.

### Why?

To keep UI smooth even during heavy updates.

Fiber handles:

* Scheduling
* Prioritizing rendering work
* Interrupting renders
* Resuming where it left off

---

# 🌍 8. **React is Declarative (Not Imperative)**

### Imperative (old way):

"Find the button, update its innerHTML."

### Declarative (React way):

“You tell what UI should look like. React updates DOM automatically.”

Example:

```jsx
{count > 5 ? <p>High</p> : <p>Low</p>}
```

React decides how to update the DOM.

---

# 🧩 9. **JSX → JavaScript → Virtual DOM**

JSX is not HTML.

This:

```jsx
<h1>Hello</h1>
```

Becomes:

```js
React.createElement("h1", null, "Hello");
```

Which becomes Virtual DOM node.

---

# 🔥 10. **React Rendering Optimization**

React uses:

* Virtual DOM diffing
* useMemo
* useCallback
* PureComponent
* Memoization
* Keyed lists

This avoids unnecessary renders.

---

# 📌 Simple Example (Full Flow)

```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Add</button>
    </div>
  );
}
```

### Flow:

1. User clicks → setCount(1)
2. state changed
3. Component re-renders
4. JSX → Virtual DOM
5. React compares old/new
6. Only `<p>` updates
7. Browser updates the UI

---

# 🎯 Summary (Super Easy)

| Concept        | Meaning                      |
| -------------- | ---------------------------- |
| Component      | Function returning UI        |
| State          | Data that triggers re-render |
| Props          | Data passed from parent      |
| Virtual DOM    | Fast memory DOM              |
| Reconciliation | Compare & update DOM         |
| Hooks          | Manage logic                 |
| Fiber          | Scheduling engine            |
| Declarative    | You describe UI              |

