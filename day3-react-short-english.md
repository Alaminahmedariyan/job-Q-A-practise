# 🔵 React Fundamentals — Study Guide & Short Answers (English)

**Day 3 Topic:** Components, Hooks & State Management

## 📘 How to study this guide

1. Read the **🎤 Say** part first. This is the answer you give in the interview.
2. In **📌 Understand it**, read the `👉` line under each point. That is the real meaning.
3. Write the **🧪 Code** yourself in a React project (Vite or Next.js) and check the result.
4. At the end, close the file and say the answer out loud in your own words.

---

## 3️⃣1️⃣ What is React and what problem does it solve?

> 🎤 **Say:** React is a JavaScript library made by Meta. We use it to build user interfaces. We break the screen into small parts called components, and we can use each part again and again. Before React, we had to change the page by hand when data changed. That was hard and often wrong. With React, I only describe how the screen should look, and React updates it when the data changes.

📌 **Understand it**

- **React is a library, not a full framework**
  👉 It only handles the screen. For other things like pages and routes, you use extra tools (Next.js, React Router).
- **Component-based**
  👉 Like Lego blocks. Make a Button once, use it everywhere.
- **Declarative**
  👉 You do not write "how to change the page". You write "if the data is like this, the screen looks like this". React does the rest.
- **Fast updates with the virtual DOM**
  👉 React does not redraw the whole page. It only changes the small part that is different.
- **One-way data flow**
  👉 Data goes from top to bottom (parent to child). So it is easy to find where a change came from.

🧪 **Code**

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Use the same component many times
<Welcome name="Alamin" />
<Welcome name="Rahim" />
```

🔮 **Today & future:** Next.js and React Native are built on React. Learning it opens the door to most modern frontend jobs.

---

## 3️⃣2️⃣ What is JSX and why is it used in React?

> 🎤 **Say:** JSX is a way to write HTML-like code inside JavaScript. The browser cannot read it directly. A tool like Babel changes it into normal JavaScript function calls. With JSX, the look of the screen and its logic stay in one place, so the code is easy to read.

📌 **Understand it**

- **JSX is not HTML**
  👉 It looks like HTML, but it is really JavaScript. In the end it becomes a call like `React.createElement`.
- **You need one root element**
  👉 To return many elements, wrap them in a `<div>` or an empty `<>...</>` (Fragment).
- **`className` instead of `class`**
  👉 `class` is a word that JavaScript already uses. So JSX uses `className`. In the same way, `for` becomes `htmlFor`.
- **Close every tag**
  👉 Write `<img />` and `<input />` with a `/` at the end.
- **Use `{ }` to put in JavaScript**
  👉 `{name}`, `{2 + 3}`, `{list.map(...)}` all work. But `if` and `for` do not work directly. Only expressions work.

🧪 **Code**

```jsx
const name = "Alamin";
const el = (
  <div className="card">
    <h2>Hello, {name}</h2>
    <p>2 + 3 = {2 + 3}</p>
    <img src="a.png" alt="photo" />
  </div>
);

// Inside, it is really this:
// React.createElement("div", { className: "card" }, ...)
```

🔮 **Today & future:** Next.js and Vite support JSX. With TypeScript it is called TSX.

---

## 3️⃣3️⃣ What is the difference between functional and class components?

> 🎤 **Say:** A functional component is a normal function that returns JSX. It uses Hooks for state and lifecycle work. A class component extends `React.Component`, has a `render()` method, and uses `this.state` and lifecycle methods. Today everyone writes functional components because they are shorter and simpler, and there is no trouble with `this`.

📌 **Understand it**

- **Functional → function + Hooks**
  👉 It uses `useState` and `useEffect` to handle state and side effects.
- **Class → `render()` + `this.state`**
  👉 It uses `this.setState()` to change state, and has methods like `componentDidMount`.
- **Class has trouble with `this`**
  👉 `this` gets lost inside methods, so you need `bind` or an arrow function. Functional components do not have this problem.
- **One exception: Error Boundary**
  👉 A component that catches errors must still be written as a class.

| Feature | Functional | Class |
|---|---|---|
| How to write | function | `class ... extends React.Component` |
| State | `useState` | `this.state` |
| Lifecycle | `useEffect` | `componentDidMount` and others |
| `this` | not needed | needed |
| Used today | ✅ Yes | in old code |

🧪 **Code**

```jsx
// Functional
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}

// Class
class CounterC extends React.Component {
  state = { count: 0 };
  render() {
    return (
      <button onClick={() => this.setState({ count: this.state.count + 1 })}>
        {this.state.count}
      </button>
    );
  }
}
```

🔮 **Today & future:** All new projects use functional components. You only need class components to read old code.

---

## 3️⃣4️⃣ What is the virtual DOM and how does React use it?

> 🎤 **Say:** The virtual DOM is a light copy of the real DOM, made as a JavaScript object. When state changes, React makes a new virtual DOM and compares it with the old one. This is called diffing. Then React updates only the changed part in the real DOM, all at once. The whole process is called reconciliation.

📌 **Understand it**

- **Changing the real DOM again and again is slow**
  👉 Each time, the browser must work out the layout and draw the page again.
- **Step 1: Make a new virtual DOM**
  👉 When state or props change, React draws a new picture of the screen in memory.
- **Step 2: Compare with the old one (diffing)**
  👉 React checks both pictures and finds what is different.
- **Step 3: Change only the difference in the real DOM**
  👉 Not the whole page, only the small part that changed. If only one text changes, only that text changes.
- **In lists, `key` helps diffing**
  👉 With keys, React knows which item is which.

🧪 **Code**

```jsx
function App() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Static title</h1>            {/* does not change, DOM is not touched */}
      <p>Count: {count}</p>            {/* only this text is updated */}
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

🔮 **Today & future:** Knowing how React draws the screen helps you find speed problems.

---

## 3️⃣5️⃣ Explain the useState hook with an example.

> 🎤 **Say:** `useState` is a hook that lets a functional component keep state. It gives back an array with two things: the current value and a function to change it. When I call the setter, the value changes and the component renders again. We cannot change state directly. We must always use the setter.

📌 **Understand it**

- **Syntax: `const [value, setValue] = useState(initial)`**
  👉 `initial` is the starting value. We use array destructuring to get the two things.
- **Calling the setter causes a re-render**
  👉 React runs the component again with the new value and updates the screen.
- **Do not change state directly**
  👉 If you write `count++` or `arr.push()`, React cannot see the change. Always use `setCount(...)`.
- **If the new value depends on the old one, use a function**
  👉 `setCount(prev => prev + 1)`. This stays correct even when many updates come together.
- **For objects and arrays, make a new copy**
  👉 `setUser({ ...user, age: 21 })`. If you change the old one, React does not notice.
- **Right after calling the setter, the state is still old**
  👉 You get the new value in the next render, not on the same line.

🧪 **Code**

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  const [user, setUser] = useState({ name: "Alamin", age: 20 });

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(prev => prev + 1)}>+1</button>
      <button onClick={() => setUser({ ...user, age: user.age + 1 })}>
        Add age ({user.age})
      </button>
    </div>
  );
}
```

🔮 **Today & future:** Forms, modals, toggles: all UI starts with `useState`.

---

## 3️⃣6️⃣ What is the useEffect hook and what are its use cases?

> 🎤 **Say:** `useEffect` lets us run side effects after the component renders. For example: getting data from an API, timers, event listeners, or changing the DOM. The second argument is the dependency array, and it decides when the effect runs. The effect can return a cleanup function. It runs when the component is removed, or before the effect runs again.

📌 **Understand it**

- **No dependency array → runs after every render**
  👉 Most of the time you do not want this. It can cause an endless loop.
- **`[]` (empty) → runs only the first time**
  👉 Used to get data once, when the page opens.
- **`[a, b]` → runs when a or b changes**
  👉 For example, get new data when an ID changes.
- **Cleanup function**
  👉 `return () => ...`. Stop a timer or remove a listener. If you do not, memory leaks can happen.
- **In dev mode, Strict Mode runs the effect two times**
  👉 This is on purpose, to check that your cleanup is right. In production it runs once.
- **If you can work out a value during render, you do not need an effect**
  👉 Use effects only for work with the outside world.

🧪 **Code**

```jsx
import { useState, useEffect } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  // 1) Get data only the first time
  useEffect(() => {
    fetch("/api/users")
      .then(res => res.json())
      .then(setUsers);
  }, []);

  // 2) Timer + cleanup
  useEffect(() => {
    const id = setInterval(() => console.log("tick"), 1000);
    return () => clearInterval(id);   // stop the timer when removed
  }, []);

  return <p>Total: {users.length}</p>;
}
```

🔮 **Today & future:** In Next.js, server components or TanStack Query are now used more for data. Still, you must understand useEffect.

---

## 3️⃣7️⃣ What is the difference between controlled and uncontrolled components?

> 🎤 **Say:** In a controlled component, the value of the input lives in React state. We control it with `value` and `onChange`, so React is the one source of truth. In an uncontrolled component, the value lives in the browser's DOM, and we read it with a `ref` when we need it. Controlled is good for checking input and instant reactions. Uncontrolled is good for simple cases and file inputs.

📌 **Understand it**

- **Controlled → `value` + `onChange`**
  👉 Each time you type a letter, the state changes, and the input shows that state.
- **Uncontrolled → read with a `ref`**
  👉 React knows nothing while you type. When you submit, you read `ref.current.value`.
- **Good side of controlled**
  👉 It is easy to check input live, turn a button on or off, and format the value.
- **File input is always uncontrolled**
  👉 You cannot set the value of `<input type="file" />` from code.
- **If you give `value` but no `onChange`, the input gets stuck**
  👉 React holds the value but there is no way to change it, so you cannot type.

🧪 **Code**

```jsx
// Controlled
function Controlled() {
  const [text, setText] = useState("");
  return <input value={text} onChange={e => setText(e.target.value)} />;
}

// Uncontrolled
function Uncontrolled() {
  const ref = useRef(null);
  return (
    <>
      <input ref={ref} defaultValue="hi" />
      <button onClick={() => alert(ref.current.value)}>Show</button>
    </>
  );
}
```

🔮 **Today & future:** In big forms, React Hook Form works in the uncontrolled way to keep things fast.

---

## 3️⃣8️⃣ What are props in React and how are they passed?

> 🎤 **Say:** Props are data that a parent component sends to a child component. We write them like HTML attributes. Props are read-only, so the child cannot change them. We can also send functions, so the child can tell the parent something. A special prop called `children` lets us send the content between the tags.

📌 **Understand it**

- **Sending: `<Card title="Hi" />`**
  👉 Write it like an attribute. The child gets it as a props object.
- **Receiving: destructuring**
  👉 `function Card({ title })`. This is cleaner than writing `props.title`.
- **Props are read-only**
  👉 A child cannot write `props.title = ...`. To change it, the parent must change its state.
- **You can send functions**
  👉 `<Button onClick={handleClick} />`. This is how a child talks to its parent.
- **The `children` prop**
  👉 If you write `<Box>inner text</Box>`, then "inner text" arrives as `children`.
- **Default value**
  👉 `function Card({ title = "Untitled" })`

🧪 **Code**

```jsx
function Card({ title, price = 0, onBuy, children }) {
  return (
    <div>
      <h3>{title} — {price} taka</h3>
      {children}
      <button onClick={onBuy}>Buy</button>
    </div>
  );
}

function App() {
  return (
    <Card title="Camera" price={500} onBuy={() => alert("Bought")}>
      <p>3 days rent</p>
    </Card>
  );
}
```

🔮 **Today & future:** With TypeScript you write the type of each prop, so mistakes are caught early.

---

## 3️⃣9️⃣ What is prop drilling and how can it be avoided?

> 🎤 **Say:** Prop drilling is when you pass data through many levels of components just to reach a deep child, even though the middle components do not need that data. It makes code messy and hard to change. To avoid it, we can use the Context API, component composition (`children`), or a state library like Redux or Zustand.

📌 **Understand it**

- **Problem: middle components are just postmen**
  👉 `App → Layout → Sidebar → Avatar`. Only Avatar needs `user`, but everyone must carry it.
- **Fix 1: Context API**
  👉 Put the data once at the top. Any child below can take it directly.
- **Fix 2: Composition**
  👉 If you send a ready-made component as `children`, there are fewer levels in the middle.
- **Fix 3: Zustand / Redux**
  👉 Keep the app data in a separate store. Anyone can take from it.
- **You do not always need to avoid it**
  👉 For 1 or 2 levels, passing props is simple and clear.

🧪 **Code**

```jsx
// ❌ Prop drilling
<Layout user={user} />
function Layout({ user }) { return <Sidebar user={user} />; }
function Sidebar({ user }) { return <Avatar user={user} />; }

// ✅ With composition
<Layout sidebar={<Avatar user={user} />} />
function Layout({ sidebar }) { return <aside>{sidebar}</aside>; }
```

🔮 **Today & future:** For app-wide data like login, theme and language, we use Context or Zustand.

---

## 4️⃣0️⃣ Explain the useContext hook with an example.

> 🎤 **Say:** `useContext` lets any deep component read shared data directly, without passing props at every level. First I make a context with `createContext`. Then I give a `value` in a Provider at the top. Below, I read it with `useContext`. It is good for global data that does not change often, like theme, logged-in user, or language.

📌 **Understand it**

- **Step 1: `createContext()`**
  👉 Make a "channel" for the data.
- **Step 2: Wrap with a `Provider`**
  👉 Put `<Ctx.Provider value={...}>` around the part that needs the data.
- **Step 3: `useContext(Ctx)`**
  👉 Any component inside gets the value directly.
- **When the value changes, all consumers render again**
  👉 So do not keep fast-changing data (like mouse position) in Context.
- **Outside a Provider you get the default value**
  👉 That is the value you gave to `createContext(defaultValue)`.

🧪 **Code**

```jsx
import { createContext, useContext, useState } from "react";

const ThemeContext = createContext("light");

function App() {
  const [theme, setTheme] = useState("dark");
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Page />
    </ThemeContext.Provider>
  );
}

function Page() { return <Button />; }   // nothing was passed

function Button() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>
      Now: {theme}
    </button>
  );
}
```

🔮 **Today & future:** In Next.js apps, Context is a very common way to share theme, login and cart.

---

## 4️⃣1️⃣ What is the useRef hook and when would you use it?

> 🎤 **Say:** `useRef` gives back an object like `{ current: ... }`. It stays the same between renders, and changing its value does not make the component render again. It has two main uses: to reach a DOM element directly (for example, to focus an input), and to keep a value that does not need to update the screen, like a timer ID.

📌 **Understand it**

- **Changing `ref.current` does not cause a re-render**
  👉 This is the big difference from `useState`. State change updates the screen. Ref change does not.
- **Get a DOM element: `<input ref={myRef} />`**
  👉 Then `myRef.current` is the real input element. You can call `.focus()` or `.scrollIntoView()`.
- **Keep a hidden value**
  👉 Things like the id of a `setInterval`, or an old value. You need them later but do not show them on screen.
- **Avoid reading or writing `ref.current` during render**
  👉 Do it inside an event handler or an effect. Otherwise the result can be unpredictable.

🧪 **Code**

```jsx
import { useRef, useState, useEffect } from "react";

function Search() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();   // cursor goes to the input when the page opens
  }, []);

  return <input ref={inputRef} placeholder="Search..." />;
}

function Timer() {
  const idRef = useRef(null);
  const [n, setN] = useState(0);

  const start = () => { idRef.current = setInterval(() => setN(x => x + 1), 1000); };
  const stop  = () => clearInterval(idRef.current);

  return (
    <>
      <p>{n}</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </>
  );
}
```

🔮 **Today & future:** Form focus, scroll, video play and pause, animation libraries: `useRef` is everywhere.

---

## 4️⃣2️⃣ What are React keys and why are they important in lists?

> 🎤 **Say:** When we show a list, each item needs a unique and stable `key`. This helps React know which item was added, removed or moved. Without keys, or with wrong keys, React can update the wrong item. This causes bugs and slow speed. We should use the data's ID as the key. We should not use the index if the order of the list can change.

📌 **Understand it**

- **A key is the item's ID card**
  👉 With the ID card, React can say "this is the same person as before, just in a new place".
- **It must be unique only among siblings**
  👉 Not in the whole app, only inside the same list.
- **It must be stable**
  👉 Using `Math.random()` is wrong. If the key is new on each render, React must rebuild every item.
- **Problem with index as key**
  👉 If you remove an item from the middle or change the order, text typed in an input can move to the wrong item.
- **When is index fine?**
  👉 When the list never changes, the order is fixed, and the items have no ID.
- **`key` does not reach the child as a prop**
  👉 It is only for React's own work.

🧪 **Code**

```jsx
const todos = [
  { id: 1, text: "Study" },
  { id: 2, text: "Play" },
];

// ✅ Correct
<ul>
  {todos.map(t => <li key={t.id}>{t.text}</li>)}
</ul>

// ❌ Risky (problem if the order changes)
{todos.map((t, i) => <li key={i}>{t.text}</li>)}
```

🔮 **Today & future:** Using the database `id` directly as the key is the easiest and safest habit.

---

## 4️⃣3️⃣ What is the difference between state and props?

> 🎤 **Say:** Props come from outside, from the parent, and the child can only read them. State lives inside the component, and the component can change it with a setter. When either one changes, the component renders again. If two components need the same data, we move the state up to their nearest common parent.

📌 **Understand it**

- **Props → borrowed**
  👉 Got from someone else. You can use them but you cannot change them.
- **State → your own**
  👉 The component's own memory. It can change it by itself.
- **One person's state is another person's props**
  👉 When a parent gives its state to a child as a prop, the child sees it as props.
- **Lifting state up**
  👉 If two siblings need the same data, move the state to their parent and send it down as props.

| Feature | Props | State |
|---|---|---|
| Where it comes from | from the parent | inside the component |
| Can it change? | No (read-only) | Yes (with a setter) |
| Who changes it | the parent | the component itself |
| When it changes | re-render | re-render |

🧪 **Code**

```jsx
function Parent() {
  const [count, setCount] = useState(0);        // state (Parent's own)
  return <Child count={count} onAdd={() => setCount(count + 1)} />;
}

function Child({ count, onAdd }) {               // props (borrowed)
  return <button onClick={onAdd}>{count}</button>;
}
```

🔮 **Today & future:** Deciding "where should this state live" is the most important skill in React design.

---

## 4️⃣4️⃣ How does conditional rendering work in React?

> 🎤 **Say:** Conditional rendering means showing different UI based on a condition. React has no special syntax for it. We use normal JavaScript: `if/else`, the ternary `? :`, and `&&`. If a component returns `null`, nothing is shown.

📌 **Understand it**

- **Early return with `if`**
  👉 Write `if (loading) return <Spinner />;` at the top, then the normal UI below.
- **Ternary: `condition ? A : B`**
  👉 When you must show one of two things. You can write it inside JSX.
- **`&&`: show if true, otherwise nothing**
  👉 `{isAdmin && <AdminPanel />}`
- **Trap with `&&`: the number `0`**
  👉 `{count && <X />}` shows `0` on screen when `count` is 0. Write `{count > 0 && <X />}` instead.
- **Return `null` → shows nothing**
  👉 When you want to hide a component on purpose.

🧪 **Code**

```jsx
function Dashboard({ loading, user, items }) {
  if (loading) return <p>Loading...</p>;      // early return

  return (
    <div>
      {user ? <h2>Welcome, {user.name}</h2> : <a href="/login">Log in</a>}
      {user?.isAdmin && <button>Admin panel</button>}
      {items.length > 0 && <p>Total {items.length} items</p>}   {/* not just length && */}
    </div>
  );
}
```

🔮 **Today & future:** Loading, error and empty states: every UI needs these 3 patterns.

---

## 4️⃣5️⃣ What is React.memo and when should you use it?

> 🎤 **Say:** `React.memo` wraps a component so that it does not render again if its props are the same as before. Normally, when a parent renders, all its children render too. `memo` stops that. It checks props with a shallow compare, so for object, array or function props we also need `useMemo` and `useCallback`. Use it only on heavy components that render often.

📌 **Understand it**

- **When the parent renders, the child renders too**
  👉 Even if the props did not change. This is extra work.
- **`memo` does a shallow compare**
  👉 It checks each prop against the old one with `===`. If all match, it skips the render.
- **Objects, arrays and functions are new on every render**
  👉 If you write `{}` or `() => {}`, you get a new reference each time, so `memo` does not help. Fix: `useMemo` and `useCallback`.
- **`memo` cannot stop renders caused by its own state or context**
  👉 It only stops renders that come from the parent.
- **Do not use it everywhere**
  👉 The compare also costs time. Measure first (React DevTools Profiler), then add it.

🧪 **Code**

```jsx
import { memo, useState, useCallback } from "react";

const Row = memo(function Row({ name, onDelete }) {
  console.log("render:", name);
  return <li>{name} <button onClick={onDelete}>X</button></li>;
});

function List() {
  const [count, setCount] = useState(0);

  // Without useCallback, this is a new function each time, so memo would not work
  const handleDelete = useCallback(() => console.log("deleted"), []);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      <ul><Row name="Alamin" onDelete={handleDelete} /></ul>
    </>
  );
}
```

🔮 **Today & future:** The new React Compiler can do this kind of memoization for you in many cases. Still, interviewers ask about the idea.
