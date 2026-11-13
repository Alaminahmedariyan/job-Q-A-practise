# 🔵 React Fundamentals — Detailed Guide (English)

**Day 3 Topic:** Components, Hooks & State Management

## 📘 How to use this file

1. Read the **🎤 Full answer**. This is the longer answer for the interview.
2. Read **📖 Step by step** to understand the idea deeply.
3. Write the **🧪 Code** yourself and run it. Reading alone is not enough.
4. Read **⚠️ Common mistakes** with care. Interviewers like to ask about these.
5. Try the **🎯 Follow-up questions**. Think of your own answer first, then read the one below.
6. For the short version, see `day3-react-short-english.md`.

---

## 3️⃣1️⃣ What is React and what problem does it solve?

> 🎤 **Full answer:** React is a free JavaScript library made by Meta. We use it to build user interfaces. The main idea is to break the screen into small parts called components. Each part works on its own, and we can use it again and again. Before React, when data changed, we had to change the page by hand, for example with `document.getElementById(...)`. When the app became big, this code became messy, and the data and the screen often did not match. With React, I only say "if the data is like this, the screen looks like this" (declarative). When the data changes, React updates only the parts of the screen that need it.

📖 **Step by step**

- **Problem 1: The screen and the data go out of sync**
  👉 When data changes, it is hard to remember every place on the screen that must change. If you forget one place, you get a bug.
- **Problem 2: You could not reuse code easily**
  👉 If the same card was needed in 10 places, you had to copy and paste it 10 times.
- **Solution 1: Declarative UI**
  👉 You write "what" you want, not "how" to do it. React works out the "how".
- **Solution 2: Components**
  👉 Build once, use many times. Change it in one place and it changes everywhere.
- **Solution 3: Virtual DOM**
  👉 React does not redraw the whole page. It updates only the part that changed.
- **Solution 4: One-way data flow**
  👉 Data goes down from parent to child. It is easy to find where something came from.

🧪 **Code**

```jsx
// Imperative (old way): change the DOM by hand
const p = document.getElementById("count");
p.textContent = Number(p.textContent) + 1;

// Declarative (React): we only say the screen depends on the data
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}
```

⚠️ **Common mistakes**

- **Calling React a framework.** React is a library. For routing and server rendering you need a framework like Next.js.
- **Thinking "React means fast".** React helps more with keeping code clean and easy to maintain than with raw speed.

🎯 **Follow-up questions**

- **What is the difference between a library and a framework?**
  👉 You call a library (you are in control). A framework calls your code (it is in control). React only gives you the UI part. The other choices are yours.
- **What is the difference between declarative and imperative?**
  👉 Imperative = step-by-step orders ("do this, then that"). Declarative = describe the result ("I want it to look like this").

📝 **Remember in one line:** Change the data, and React changes the screen.

🔮 **Today & future:** Next.js, React Native and Remix are all built on React.

---

## 3️⃣2️⃣ What is JSX and why is it used in React?

> 🎤 **Full answer:** JSX (JavaScript XML) is a special way to write JavaScript. It lets us write HTML-like code inside a JavaScript file. The browser cannot read JSX. A tool like Babel or SWC changes it into normal JavaScript function calls. We use JSX because the look of the screen and its logic stay in the same component, so the code is easy to read and understand. You can write React without JSX, but the code becomes much longer and harder to read.

📖 **Step by step**

- **Step 1: You write JSX**
  👉 `<h1 className="title">Hi</h1>`
- **Step 2: A tool changes it into JavaScript**
  👉 Code like `React.createElement("h1", { className: "title" }, "Hi")` (in new versions, a `jsx()` function).
- **Step 3: It gives back a plain object**
  👉 This object is a piece of the Virtual DOM.
- **The rules of JSX**
  👉 One root element, close every tag, `className`, `htmlFor`, and camelCase attributes (`onClick`, `tabIndex`).
- **Only expressions go inside `{ }`**
  👉 `{a + b}`, `{cond ? x : y}`, `{list.map(...)}` work. `if`, `for` and `const` do not.
- **Styles need an object**
  👉 `style={{ color: "red", fontSize: 20 }}`. The outer `{}` is JavaScript, the inner `{}` is an object.

🧪 **Code**

```jsx
function Profile() {
  const user = { name: "Alamin", skills: ["JS", "React"] };

  return (
    // Wrap many elements in a Fragment
    <>
      <h1 className="title" style={{ color: "teal" }}>
        {user.name}
      </h1>

      <label htmlFor="email">Email</label>
      <input id="email" type="email" />

      <ul>
        {user.skills.map(s => <li key={s}>{s}</li>)}
      </ul>
    </>
  );
}
```

⚠️ **Common mistakes**

- **Writing `class`.** In JSX you must write `className`.
- **Not closing a tag.** Write `<input />`, not `<input>`.
- **Writing `if` inside `{}`.** It is a statement, not an expression. Use a ternary or `&&`.
- **Showing an object directly.** `{user}` gives an error. Write `{user.name}`.

🎯 **Follow-up questions**

- **Is JSX required?**
  👉 No. You can use `React.createElement`, but nobody does.
- **Why do we need a Fragment?**
  👉 To return many elements without adding an extra `<div>`.
- **Is JSX safe from XSS attacks?**
  👉 Yes. React escapes values put inside `{ }` automatically. But if you use `dangerouslySetInnerHTML`, that safety is gone.

📝 **Remember in one line:** JSX looks like HTML, but it is really JavaScript.

🔮 **Today & future:** With TypeScript it is TSX, and server components use the same syntax.

---

## 3️⃣3️⃣ What is the difference between functional and class components?

> 🎤 **Full answer:** A functional component is a normal JavaScript function that takes props and returns JSX. Since React 16.8 brought Hooks, functional components can also have state, lifecycle work and everything else. A class component extends `React.Component`, needs a `render()` method and keeps state in `this.state`. Today everyone writes functional components because the code is shorter, there is no trouble with `this`, and we can reuse logic with custom hooks. But an error boundary must still be a class, and old projects still have class code.

📖 **Step by step**

- **Keeping state**
  👉 Functional: `useState`. Class: `this.state` and `this.setState`.
- **Lifecycle**
  👉 Class has many methods (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`). Functional does it all with `useEffect`.
- **The `this` problem**
  👉 In a class, `this` gets lost inside event handlers, so you need `bind` or an arrow function.
- **Reusing logic**
  👉 In classes you needed HOCs or render props, which are hard to read. In functional components, a custom hook does it simply.
- **Shorter code**
  👉 The same work takes about half the lines in a functional component.

| Feature | Functional | Class |
|---|---|---|
| How to write | function | `class ... extends React.Component` |
| State | `useState` | `this.state` |
| Lifecycle | `useEffect` | many separate methods |
| `this` | not needed | needed |
| Share logic | custom hook | HOC / render props |
| Error Boundary | cannot make one | can make one |
| Used today | ✅ | in old code |

🧪 **Code**

```jsx
// Functional: get data + state
function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("/api/users").then(r => r.json()).then(setUsers);
  }, []);

  return <p>{users.length} users</p>;
}

// Class: the same work
class UsersC extends React.Component {
  state = { users: [] };

  componentDidMount() {
    fetch("/api/users").then(r => r.json()).then(users => this.setState({ users }));
  }

  render() {
    return <p>{this.state.users.length} users</p>;
  }
}
```

⚠️ **Common mistakes**

- **Saying "functional components have no state".** That was true before Hooks. Now they do.
- **Forgetting to bind a method in a class.** Then `this.setState` does not work.

🎯 **Follow-up questions**

- **Will class components stop working?**
  👉 No, React still supports them. But it is not advised for new code.
- **Is `useEffect` a direct replacement for lifecycle methods?**
  👉 Not exactly. It is about "synchronizing": keeping the outside world in line with your state.

📝 **Remember in one line:** New code = functional + Hooks.

🔮 **Today & future:** If you get a job on an old project, you will need to read class code.

---

## 3️⃣4️⃣ What is the virtual DOM and how does React use it?

> 🎤 **Full answer:** The virtual DOM is a light copy of the real DOM, kept in memory as a JavaScript object. When state or props change, React builds a new virtual DOM tree and compares it with the old one. This comparison is called diffing. Then React applies only the changes to the real DOM, together in one batch. The whole process is called reconciliation. This way we can update the UI well without touching the DOM ourselves.

📖 **Step by step**

- **Step 1: Render**
  👉 The component runs, and a tree of React elements (the virtual DOM) is made from the JSX.
- **Step 2: Diff**
  👉 The new tree is compared with the old tree.
- **Step 3: Commit**
  👉 Only the differences are applied to the real DOM.
- **Two main rules of diffing**
  👉 (1) If the element type is different (for example `div` to `span`), React rebuilds the whole subtree. (2) In lists, React uses `key` to know which item is which.
- **Batching**
  👉 Many state updates together cause only one render.
- **Fiber**
  👉 React's new inside engine. It splits work into small pieces so the browser does not get stuck.

🧪 **Code**

```jsx
function App() {
  const [count, setCount] = useState(0);
  console.log("App rendered");

  return (
    <div>
      <h1>Static title</h1>        {/* did not change → DOM is not touched */}
      <p>Count: {count}</p>        {/* changed → only this text is updated */}
      <button onClick={() => setCount(c => c + 1)}>+</button>
    </div>
  );
}
// Open the Elements tab in DevTools. When you click the button, only the <p> text flashes.
```

⚠️ **Common mistakes**

- **Saying "the virtual DOM is faster than the real DOM".** It is actually extra work. The benefit is that we do not have to change the DOM ourselves, and React smartly changes less.
- **Mixing up the virtual DOM and the shadow DOM.** The shadow DOM is a browser feature (to keep CSS separate). The virtual DOM is a React technique.

🎯 **Follow-up questions**

- **What is reconciliation?**
  👉 The process of comparing the old and new virtual DOM and deciding what to change.
- **Why do we need keys?**
  👉 To know the items in a list, so React does not rebuild every item for no reason.

📝 **Remember in one line:** Compare, then update only the difference.

🔮 **Today & future:** This idea helps you understand speed problems (why something renders again and again).

---

## 3️⃣5️⃣ Explain the useState hook with an example.

> 🎤 **Full answer:** `useState` is a React Hook that lets a functional component keep its own state. When I write `const [value, setValue] = useState(initial)`, I get two things: the current value and a function to change it. When I call the setter, React saves the new value and renders the component again, so the screen updates. We cannot change state directly, because then React cannot see the change. To change an object or an array, we always make a new copy. When the new value depends on the old one, we use the form `setX(prev => ...)`.

📖 **Step by step**

- **First render:** `useState(0)` takes 0 as the starting value.
- **Next renders:** React gives back the saved value. It does not use the starting value again.
- **When you call the setter:** React puts the work in a queue, then runs the component again with the new value.
- **The snapshot idea**
  👉 In each render, state is like a fixed "photo". Inside one render, `count` does not change. That is why writing `setCount(count + 1)` three times adds only 1.
- **Functional update**
  👉 Writing `setCount(c => c + 1)` three times adds 3, because each one starts from the latest value.
- **Lazy initial state**
  👉 For heavy work, write `useState(() => heavyWork())`. It then runs only the first time.
- **Objects and arrays: update without changing the old one**
  👉 `{ ...obj, key: new }`, `[...arr, item]`, `arr.filter(...)`, `arr.map(...)`.

🧪 **Code**

```jsx
import { useState } from "react";

function Demo() {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([]);
  const [form, setForm] = useState({ name: "", age: 0 });

  const addThree = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);          // only +1 (all of them see the same old count)
  };

  const addThreeRight = () => {
    setCount(c => c + 1);
    setCount(c => c + 1);
    setCount(c => c + 1);         // +3 ✅
  };

  const addTodo = text => setTodos([...todos, { id: Date.now(), text }]);
  const removeTodo = id => setTodos(todos.filter(t => t.id !== id));
  const setName = name => setForm({ ...form, name });

  return (
    <div>
      <p>{count}</p>
      <button onClick={addThree}>Wrong</button>
      <button onClick={addThreeRight}>Right</button>
    </div>
  );
}
```

⚠️ **Common mistakes**

- **Changing state directly.** If you do `todos.push(x)` or `form.name = "A"`, the screen does not update.
- **Expecting the new value right after the setter.** `setCount(5); console.log(count);` shows the old value.
- **Keeping derived data in a separate state.** Work out `fullName` straight from `first + last`. Do not make a new state for it.
- **Calling a Hook inside a condition or a loop.** Always call Hooks at the very top level of the component.

🎯 **Follow-up questions**

- **If I set the same value, does it render again?**
  👉 React compares with `Object.is`. If the value is the same, it usually skips the render.
- **Is state async?**
  👉 The setter returns nothing, and updates are batched. So you get the new value in the next render.
- **`useState` or `useReducer`?**
  👉 For simple values, `useState`. For many related states or complex update rules, `useReducer`.

📝 **Remember in one line:** Do not change state yourself. Give the setter a new copy.

🔮 **Today & future:** Forms, modals, filters, toggles: it is the base of every interactive UI.

---

## 3️⃣6️⃣ What is the useEffect hook and what are its use cases?

> 🎤 **Full answer:** `useEffect` is a Hook that lets us run side effects after the component renders. A side effect is work outside of rendering: getting data from an API, running a timer or subscription, adding an event listener, changing `document.title`, and so on. The second argument, the dependency array, decides when the effect runs. The effect can return a cleanup function. It runs when the component is removed, or before the next effect runs, so we avoid memory leaks.

📖 **Step by step**

- **When does it run?**
  👉 After React has drawn the screen.
- **Three forms of the dependency array**
  👉 (1) No array: after every render. (2) `[]`: only the first time. (3) `[x, y]`: the first time, and again when x or y changes.
- **When does cleanup run?**
  👉 Before the next effect runs, and when the component is removed.
- **Stale closure**
  👉 Any state or props you use inside the effect must be in the dependency list. If not, an old value can get stuck.
- **Race condition**
  👉 If the ID changes fast, an old request can come back late and cover the new data. To avoid this, use a flag or `AbortController` in the cleanup.
- **Strict Mode**
  👉 In development, effects run two times. This is to check that your cleanup is right.
- **When you do not need useEffect**
  👉 For values you can work out during render, or for reactions to a click (those go in event handlers).

🧪 **Code**

```jsx
import { useState, useEffect } from "react";

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // 1) Get data (again when userId changes), and handle the race condition
  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);

    fetch(`/api/users/${userId}`, { signal: controller.signal })
      .then(r => r.json())
      .then(data => { setUser(data); setLoading(false); })
      .catch(err => { if (err.name !== "AbortError") console.error(err); });

    return () => controller.abort();   // cancel the old request
  }, [userId]);

  // 2) Event listener + cleanup
  useEffect(() => {
    const onResize = () => console.log(window.innerWidth);
    window.addEventListener("resize", onResize);
    return () => window.removeEventListener("resize", onResize);
  }, []);

  // 3) Document title
  useEffect(() => {
    if (user) document.title = user.name;
  }, [user]);

  if (loading) return <p>Loading...</p>;
  return <h2>{user.name}</h2>;
}
```

⚠️ **Common mistakes**

- **Forgetting the dependency array.** Writing `useEffect(() => { setX(...) })` can cause an endless loop.
- **No cleanup.** Timers or listeners stay alive, and memory leaks happen.
- **Cheating on dependencies.** Hiding the warning with `// eslint-disable` brings old-value bugs.
- **Giving an `async` function directly to the effect.** `useEffect(async () => ...)` is wrong, because an effect may return a cleanup function, not a Promise. Make a separate async function inside and call it.

🎯 **Follow-up questions**

- **What is the difference between `useEffect` and `useLayoutEffect`?**
  👉 `useLayoutEffect` runs before the screen is drawn (to measure the DOM). `useEffect` runs after.
- **Is useEffect the best way to get data?**
  👉 No. TanStack Query, SWR or Next.js server components give you caching, retry and loading states for free.
- **Why does my effect run twice?**
  👉 Strict Mode, in development only.

📝 **Remember in one line:** useEffect = keep in sync with the outside world, and do not forget cleanup.

🔮 **Today & future:** Modern apps use it less, but you must know how to use it well.

---

## 3️⃣7️⃣ What is the difference between controlled and uncontrolled components?

> 🎤 **Full answer:** In a controlled component, the value of the form element (input, textarea, select) lives in React state. We show the value with the `value` prop, and we write every change into state with `onChange`. So React is the one source of truth. In an uncontrolled component, the value lives in the browser's DOM. We give a starting value with `defaultValue`, and we read the value with a `ref` when we need it. With controlled components, it is easy to check input live, format the value, and turn buttons on or off. Uncontrolled components need less code, and a file input is always uncontrolled.

📖 **Step by step**

- **The controlled cycle**
  👉 The user types → `onChange` runs → state changes → React renders again → the input shows the new value.
- **The uncontrolled cycle**
  👉 The user types → the browser keeps the value → React knows nothing → when submitting, we read `ref.current.value`.
- **`value` vs `defaultValue`**
  👉 `value` = React controls it (controlled). `defaultValue` = only a starting value (uncontrolled).
- **When to use which**
  👉 Live checking, fields that depend on each other, or formatting → controlled. Small simple forms or file upload → uncontrolled.
- **Speed**
  👉 Controlled renders on every letter. In big forms, React Hook Form (which works in an uncontrolled way) reduces this problem.
- **Do not switch between controlled and uncontrolled**
  👉 If `value` was `undefined` first and then gets a value, React warns you. Start with `""`.

🧪 **Code**

```jsx
import { useState, useRef } from "react";

// Controlled: with live checking
function SignupControlled() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const valid = email.includes("@") && password.length >= 6;

  const handleSubmit = e => {
    e.preventDefault();
    console.log({ email, password });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={email} onChange={e => setEmail(e.target.value)} placeholder="Email" />
      <input type="password" value={password}
             onChange={e => setPassword(e.target.value)} placeholder="Password" />
      {!valid && <p>Email needs @ and password needs 6+ letters</p>}
      <button disabled={!valid}>Submit</button>
    </form>
  );
}

// Uncontrolled: read with a ref
function SignupUncontrolled() {
  const emailRef = useRef(null);
  const fileRef = useRef(null);

  const handleSubmit = e => {
    e.preventDefault();
    console.log(emailRef.current.value, fileRef.current.files[0]);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input ref={emailRef} defaultValue="" />
      <input type="file" ref={fileRef} />
      <button>Submit</button>
    </form>
  );
}
```

⚠️ **Common mistakes**

- **Giving `value` without `onChange`.** The input gets stuck and you cannot type.
- **Not using `checked` for a checkbox.** A checkbox needs `checked` and `onChange`.
- **Forgetting `e.preventDefault()`.** The page reloads when you submit the form.

🎯 **Follow-up questions**

- **Does a controlled component always need `useState`?**
  👉 The value must come from React state or an outside store. `useState` is the most common way.
- **Why is a file input uncontrolled?**
  👉 For safety, the browser does not let code set the value of a file input.

📝 **Remember in one line:** Controlled = React holds the value. Uncontrolled = the DOM holds the value.

🔮 **Today & future:** React Hook Form + Zod is now almost the standard pair.

---

## 3️⃣8️⃣ What are props in React and how are they passed?

> 🎤 **Full answer:** Props (properties) are input data sent from a parent component to a child component. We write them like HTML attributes in JSX, and the child gets them as one object. Props are read-only. This means the child cannot change them, because data flows one way (from top to bottom). We can send strings, numbers, objects, arrays, functions, and even JSX as props. By sending a function, the child can tell the parent that something happened. `children` is a special prop that holds the content between the tags.

📖 **Step by step**

- **Step 1: Sending**
  👉 `<Card title="Hi" price={500} />`. Use `""` for strings and `{}` for everything else.
- **Step 2: Receiving**
  👉 `function Card(props)` or with destructuring `function Card({ title, price })`.
- **Default value**
  👉 `({ price = 0 })`. It works only when the value is `undefined`.
- **Sending with spread**
  👉 `<Card {...data} />` means every key of the object becomes a prop.
- **Sending a function (callback prop)**
  👉 `onDelete={() => remove(id)}`. When the child calls it, the parent's code runs.
- **`children`**
  👉 `<Modal><p>Inner content</p></Modal>`. Very useful for making layout components.
- **When props change, the child renders again**
  👉 If the parent gives new props, the child renders again.
- **Changing props is not allowed**
  👉 You cannot do `props.name = "X"`. To change it, the parent must change its state.

🧪 **Code**

```jsx
// Child: destructuring + default + callback + children
function ProductCard({ name, price = 0, inStock = true, onBuy, children }) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>{price} taka {inStock ? "" : "(sold out)"}</p>
      {children}
      <button disabled={!inStock} onClick={() => onBuy(name)}>Buy</button>
    </div>
  );
}

// Parent
function Shop() {
  const [cart, setCart] = useState([]);
  const products = [
    { id: 1, name: "Camera", price: 500, inStock: true },
    { id: 2, name: "Tripod", price: 200, inStock: false },
  ];

  return (
    <div>
      {products.map(p => (
        <ProductCard key={p.id} {...p} onBuy={n => setCart([...cart, n])}>
          <small>3 days rent</small>
        </ProductCard>
      ))}
      <p>In cart: {cart.length}</p>
    </div>
  );
}
```

⚠️ **Common mistakes**

- **Trying to change props.** This is against the rules of React.
- **Copying props into state.** `useState(props.value)` takes the value only the first time. When props change later, state does not change. Use props directly, or change the `key` to reset the component.
- **Calling the function while passing it.** `onClick={handle()}` is wrong (it runs right away). `onClick={handle}` or `onClick={() => handle(x)}` is right.
- **Sending a number as a string.** `price="500"` is not the same as `price={500}`.

🎯 **Follow-up questions**

- **Can props be of any type?**
  👉 Yes, even functions and JSX.
- **How do you check the type of props?**
  👉 TypeScript (most common), or the old `PropTypes`.
- **How do you send data from child to parent?**
  👉 The parent sends a callback function as a prop, and the child calls it with the data.

📝 **Remember in one line:** Props go down, events (callbacks) go up.

🔮 **Today & future:** Component libraries (shadcn/ui, MUI) are all built on props.

---

## 3️⃣9️⃣ What is prop drilling and how can it be avoided?

> 🎤 **Full answer:** Prop drilling is when you pass a piece of data through every component in the middle, just to reach a component far below, even though the middle components do not need that data themselves. This makes the middle components more complex for no reason. If the name of the data changes, many files must change, and the code is harder to understand. There are three main ways to avoid it: the Context API, component composition (`children` or a JSX prop), and a state library like Zustand or Redux.

📖 **Step by step**

- **Example:** `App → Dashboard → Sidebar → UserMenu → Avatar`
  👉 Only Avatar needs `user`, but Dashboard, Sidebar and UserMenu must all carry it.
- **Fix 1: Context API**
  👉 Put `user` in `UserContext.Provider` at the top. Avatar takes it directly with `useContext`. Nobody in the middle knows about it.
- **Fix 2: Composition**
  👉 `<Dashboard avatar={<Avatar user={user} />} />`. Avatar is made at the top, where `user` already is, so nothing needs to pass through the middle.
- **Fix 3: State library**
  👉 With Zustand, write `const user = useStore(s => s.user)` and take it from anywhere.
- **Fix 4: Custom hook**
  👉 Make a `useUser()` hook and hide the Context or store inside it.
- **When drilling is fine**
  👉 For 1 or 2 levels. Making extra Contexts is needless extra work.

🧪 **Code**

```jsx
// ❌ Prop drilling
function App() { const user = { name: "Alamin" }; return <Dashboard user={user} />; }
function Dashboard({ user }) { return <Sidebar user={user} />; }
function Sidebar({ user }) { return <Avatar user={user} />; }
function Avatar({ user }) { return <span>{user.name}</span>; }

// ✅ Fix 1: Context
const UserContext = createContext(null);

function App() {
  const user = { name: "Alamin" };
  return (
    <UserContext.Provider value={user}>
      <Dashboard />
    </UserContext.Provider>
  );
}
function Dashboard() { return <Sidebar />; }
function Sidebar() { return <Avatar />; }
function Avatar() {
  const user = useContext(UserContext);
  return <span>{user.name}</span>;
}

// ✅ Fix 2: Composition
function App2() {
  const user = { name: "Alamin" };
  return <Dashboard avatar={<Avatar2 user={user} />} />;
}
function Dashboard({ avatar }) { return <aside>{avatar}</aside>; }
function Avatar2({ user }) { return <span>{user.name}</span>; }
```

⚠️ **Common mistakes**

- **Making a Context for everything.** When a Context changes, all its consumers render again. Many Contexts are also hard to maintain.
- **Putting fast-changing data in Context.** Speed gets worse.
- **Thinking "Context = state management".** Context is only a way to deliver data. State is kept by `useState` or `useReducer`.

🎯 **Follow-up questions**

- **What is the downside of Context?**
  👉 When the value changes, all consumers render. In big apps, Zustand or Redux gives finer control.
- **How does composition reduce drilling?**
  👉 The middle components receive ready-made JSX instead of data, so they do not need to carry the data.

📝 **Remember in one line:** The one who needs the data takes it directly. Nobody in the middle is a postman.

🔮 **Today & future:** Auth, theme, cart and language are usually kept in Context or Zustand.

---

## 4️⃣0️⃣ Explain the useContext hook with an example.

> 🎤 **Full answer:** The `useContext` Hook lets a component read shared data directly from the nearest Provider above it, without passing props through the levels in between. It has three steps: first I make a context with `createContext`, then I put the data in the `value` of `Context.Provider` at the top, and in any component below I read it with `useContext(Context)`. When the Provider's `value` changes, all consumer components render again. So it is good for global data that does not change often, like theme, logged-in user and language, but not for data that changes very often.

📖 **Step by step**

- **Step 1: Make the context**
  👉 `const AuthContext = createContext(null);`
- **Step 2: Make a Provider component**
  👉 Keep the state and logic in one place and give it in `value`. Usually it is a separate component called `AuthProvider`.
- **Step 3: Make a custom hook**
  👉 Hide `useContext` inside a `useAuth()` hook. Throw an error if it is used outside the Provider.
- **Step 4: Use it**
  👉 `const { user, login } = useAuth();`
- **How re-rendering works**
  👉 When `value` changes, all consumers render. If you make a new object every time (`value={{...}}`), everyone renders for no reason, so it is good to keep it stable with `useMemo`.
- **Keep several Contexts separate**
  👉 Keep theme and auth in different Contexts, so that when one changes, the consumers of the other do not render.

🧪 **Code**

```jsx
import { createContext, useContext, useState, useMemo } from "react";

// 1) context
const AuthContext = createContext(null);

// 2) Provider
export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = name => setUser({ name });
  const logout = () => setUser(null);

  // keep value stable, to avoid needless re-renders
  const value = useMemo(() => ({ user, login, logout }), [user]);

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}

// 3) custom hook
export function useAuth() {
  const ctx = useContext(AuthContext);
  if (!ctx) throw new Error("Use useAuth only inside AuthProvider");
  return ctx;
}

// 4) usage
function App() {
  return (
    <AuthProvider>
      <Navbar />
    </AuthProvider>
  );
}

function Navbar() {
  const { user, login, logout } = useAuth();
  return user ? (
    <button onClick={logout}>{user.name}, log out</button>
  ) : (
    <button onClick={() => login("Alamin")}>Log in</button>
  );
}
```

⚠️ **Common mistakes**

- **Calling `useContext` outside the Provider.** You only get the default value (or `null`), so the code breaks.
- **Giving a new `value` object on every render.** All consumers render for no reason.
- **Keeping everything in one huge Context.** Small separate Contexts are better.
- **Thinking Context replaces `useState`.** If the state is for one component only, you do not need Context.

🎯 **Follow-up questions**

- **What is the difference between Context and Redux?**
  👉 Context is a way to deliver data. Redux is full state management (store, actions, devtools, middleware).
- **How do you avoid needless renders in consumers?**
  👉 Split the Context, keep the value stable with `useMemo`, or use a library with selectors (Zustand).
- **Where do you put Context in the Next.js App Router?**
  👉 Put the Provider in a separate client component marked `"use client"`.

📝 **Remember in one line:** create → provide → use.

🔮 **Today & future:** Almost every app has at least one `ThemeProvider` or `AuthProvider`.

---

## 4️⃣1️⃣ What is the useRef hook and when would you use it?

> 🎤 **Full answer:** `useRef` is a Hook that gives back an object shaped like `{ current: initialValue }`. This object stays the same across all renders, and when `ref.current` changes, the component does not render again. It has two main uses. First, to reach a DOM element directly, for example to focus an input, to scroll, or to play a video. Second, to keep a value that changes over time but does not need to show on screen, like a timer ID, an old value, or a flag.

📖 **Step by step**

- **Shape:** `const ref = useRef(0);` → `ref.current` is 0.
- **`useState` vs `useRef`**
  👉 When state changes, the UI updates. When a ref changes, it does not. If you need to show it on screen, use state. If not, use a ref.
- **Use 1: Get a DOM element**
  👉 If you write `<input ref={inputRef} />`, then after render `inputRef.current` is the real DOM element.
- **Use 2: Timer ID**
  👉 If you keep the ID from `setInterval` in a ref, you can call `clearInterval` later.
- **Use 3: Remember the old value**
  👉 Write `prev.current = value` in an effect, and you get the old value in the next render.
- **Use 4: Know the first render**
  👉 Keep an `isFirst` flag in a ref.
- **When to read or write**
  👉 In an event handler or an effect. Not during render.
- **To get a child's DOM**
  👉 In React 19 you can send `ref` directly as a prop. In older versions you needed `forwardRef`.

🧪 **Code**

```jsx
import { useRef, useState, useEffect } from "react";

// 1) Get the DOM: focus and scroll
function CommentBox() {
  const inputRef = useRef(null);
  const bottomRef = useRef(null);
  const [list, setList] = useState([]);

  useEffect(() => { inputRef.current.focus(); }, []);

  const add = () => {
    setList([...list, inputRef.current.value]);
    inputRef.current.value = "";
    inputRef.current.focus();
  };

  useEffect(() => {
    bottomRef.current?.scrollIntoView({ behavior: "smooth" });
  }, [list]);

  return (
    <div>
      <ul>{list.map((t, i) => <li key={i}>{t}</li>)}</ul>
      <div ref={bottomRef} />
      <input ref={inputRef} placeholder="Comment" />
      <button onClick={add}>Send</button>
    </div>
  );
}

// 2) Keep a value: stopwatch
function Stopwatch() {
  const [sec, setSec] = useState(0);
  const idRef = useRef(null);

  const start = () => {
    if (idRef.current) return;          // if already running, do not start again
    idRef.current = setInterval(() => setSec(s => s + 1), 1000);
  };
  const stop = () => {
    clearInterval(idRef.current);
    idRef.current = null;
  };

  useEffect(() => stop, []);            // stop when the component is removed

  return (
    <>
      <p>{sec} seconds</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </>
  );
}

// 3) Old value
function usePrevious(value) {
  const ref = useRef();
  useEffect(() => { ref.current = value; }, [value]);
  return ref.current;
}
```

⚠️ **Common mistakes**

- **Keeping a value you want to show on screen in a ref.** The screen does not change when a ref changes.
- **Changing `ref.current` during render.** The result can be unpredictable.
- **`ref.current` is null on the first render.** If you use a DOM ref before `useEffect`, you get null.
- **Using `document.querySelector` for everything.** In React, use `ref`.

🎯 **Follow-up questions**

- **Is `useRef` a replacement for state?**
  👉 No. When a ref changes, there is no re-render.
- **Why does changing a ref not cause a render?**
  👉 React only watches changes in state and props.
- **What is `forwardRef`?**
  👉 In old React, it was a way to pass the parent's ref to the DOM inside a child component.

📝 **Remember in one line:** A ref is a box that does not change the screen when it changes.

🔮 **Today & future:** It is needed for animation, video players, form focus, and connecting third-party libraries.

---

## 4️⃣2️⃣ What are React keys and why are they important in lists?

> 🎤 **Full answer:** When we show a list, every item needs a `key` prop. A key is a unique and stable ID. React uses it to know which item was added, removed or moved. With the right keys, React updates only the changed items and keeps the state of the other items safe. With wrong keys (for example, an index in a list whose order changes), React can put old state on the wrong item. This causes bugs and extra work. The best key is the data's own ID.

📖 **Step by step**

- **What happens without keys?**
  👉 React shows a warning, and it matches items by their order, which is often wrong.
- **How does a key work?**
  👉 During diffing, React matches items with the same key in the old and new list. If the key matches, it is "the same item as before".
- **3 qualities of a good key**
  👉 Unique (among siblings), stable (does not change between renders), predictable (not `Math.random()`).
- **Why is index a problem?**
  👉 Three items: A(0), B(1), C(2). If A is removed, B becomes 0 and C becomes 1. React thinks 0 and 1 are the same as before, so the state inside (for example, text in an input) stays in the old place. Then the wrong state sticks to the wrong item.
- **When is index safe?**
  👉 When the list is fixed, never changes, the order never changes, and the items have no ID.
- **Reset a component with a key**
  👉 When the key changes, React removes the old component and makes a new one. This is useful to reset state.
- **Where to put the key**
  👉 On the outermost element that `map` returns. For a Fragment, write `<Fragment key=...>`.

🧪 **Code**

```jsx
import { useState, Fragment } from "react";

function TodoList() {
  const [todos, setTodos] = useState([
    { id: "a1", text: "Study" },
    { id: "b2", text: "Play" },
    { id: "c3", text: "Sleep" },
  ]);

  const remove = id => setTodos(todos.filter(t => t.id !== id));

  return (
    <ul>
      {todos.map(t => (
        // ✅ key from a stable ID
        <li key={t.id}>
          <input defaultValue={t.text} />
          <button onClick={() => remove(t.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}

// ❌ index key: if you delete the first one, the text in an input can move to the wrong item
// {todos.map((t, i) => <li key={i}>...</li>)}

// Key on a Fragment
function Glossary({ items }) {
  return (
    <dl>
      {items.map(i => (
        <Fragment key={i.id}>
          <dt>{i.term}</dt>
          <dd>{i.meaning}</dd>
        </Fragment>
      ))}
    </dl>
  );
}

// Reset a component by changing the key
// <Profile key={userId} userId={userId} />
```

⚠️ **Common mistakes**

- **`key={Math.random()}`.** The key is new on every render, so all items are deleted and built again.
- **Using index when you add, delete or sort the list.** State gets mixed up.
- **Putting the key on an element inside `<li>`.** The key goes on the outermost element in `map`.
- **Trying to read the key as a prop.** `props.key` is not available.

🎯 **Follow-up questions**

- **Must a key be unique in the whole app?**
  👉 No, only among siblings under the same parent.
- **What if there is no ID?**
  👉 Make the ID when you create the data, with `crypto.randomUUID()`. Do not make it during render.
- **How does a key reset state?**
  👉 When the key changes, React thinks it is a brand new component, so it throws away the old state.

📝 **Remember in one line:** A key is the item's stable identity. Use an ID, not an index.

🔮 **Today & future:** Using the database `id` directly as the key is the safest habit.

---

## 4️⃣3️⃣ What is the difference between state and props?

> 🎤 **Full answer:** Props are data sent from parent to child, and the child can only read them, not change them. State is the component's own data. The component itself can change it with a setter, and when it changes, the component renders again. The owner of props is the parent, and the owner of state is the component itself. Both affect the UI and both cause a re-render when they change. If two or more components need the same data, we move the state up to their nearest common parent (lifting state up) and send it down as props.

📖 **Step by step**

- **Ownership**
  👉 Props belong to the parent. State belongs to the component itself.
- **Changing**
  👉 Only the parent can change props. The component changes state by itself with `setState`.
- **The same data, two faces**
  👉 What is state in the parent is props in the child.
- **Re-render**
  👉 When state or props change, the component renders.
- **Lifting state up**
  👉 If two sibling components want the same data, the state is moved to their parent.
- **When state, when props, when neither**
  👉 Changes over time and must show on screen → state. Someone else gives it → props. Can be worked out from other state or props → neither, just work it out.

| Feature | Props | State |
|---|---|---|
| Owner | parent | the component itself |
| Can it change? | No (read-only) | Yes (with a setter) |
| Purpose | send data or functions | keep the component's own changing data |
| When it changes | re-render | re-render |
| Example | `<Card title="Hi" />` | `useState(0)` |

🧪 **Code**

```jsx
// Lifting state up: two siblings show the same temperature
function Converter() {
  const [celsius, setCelsius] = useState(0);        // state is here

  return (
    <>
      <CelsiusInput value={celsius} onChange={setCelsius} />
      <FahrenheitView celsius={celsius} />
    </>
  );
}

function CelsiusInput({ value, onChange }) {         // props
  return <input type="number" value={value} onChange={e => onChange(Number(e.target.value))} />;
}

function FahrenheitView({ celsius }) {               // props
  const f = celsius * 9 / 5 + 32;                    // worked out, not a separate state
  return <p>{f} °F</p>;
}
```

⚠️ **Common mistakes**

- **Changing props directly.** In a child you cannot do `props.value = 5`.
- **Keeping derived data in a separate state.** If you make `fahrenheit` a separate state, the two can get out of sync.
- **Lifting state too high.** Lift it only as far as needed. Otherwise everything renders for no reason.

🎯 **Follow-up questions**

- **How does a child change the parent's state?**
  👉 The parent gives a callback function as a prop, and the child calls it.
- **When props change, is the child's state reset?**
  👉 No. The state stays. It resets only when the `key` changes.
- **Are props and state both async?**
  👉 Props come from the parent, and state updates are batched. Both are fixed inside a render's snapshot.

📝 **Remember in one line:** Props = borrowed. State = your own.

🔮 **Today & future:** Deciding "where should this state live" is the main skill in React design.

---

## 4️⃣4️⃣ How does conditional rendering work in React?

> 🎤 **Full answer:** Conditional rendering means showing different UI based on a condition. React has no special syntax for it. Plain JavaScript works. I use `if/else` for an early return, the ternary `condition ? A : B` inside JSX, and `&&` for the "show it or show nothing" case. If a component returns `null`, `false` or `undefined`, nothing is shown. When I use `&&`, if the left side is `0`, the screen prints `0`. So I always write a true/false condition (`count > 0`).

📖 **Step by step**

- **Way 1: `if` + early return**
  👉 Handle special states like `loading`, `error` and empty data first, then write the main UI.
- **Way 2: Ternary**
  👉 One of two: `{isLoggedIn ? <Home /> : <Login />}`.
- **Way 3: `&&`**
  👉 Show a part or do not show it: `{error && <ErrorMsg />}`.
- **Way 4: Keep it in a variable**
  👉 `let content; if (...) content = <A />; else content = <B />;` then `{content}`.
- **Way 5: Many states with an object or switch**
  👉 If there are 4 or 5 kinds of UI based on `status`, a `switch` or a lookup object is cleaner.
- **Returning `null`**
  👉 The component itself decides to show nothing.
- **Hiding with CSS vs not rendering**
  👉 With `display: none`, the component stays (its state stays). If you do not render it with a condition, the component is removed (it loses its state).
- **The 4-state pattern**
  👉 loading → error → empty → data. Handle each one separately.

🧪 **Code**

```jsx
function Orders({ loading, error, orders, user }) {
  // early return: all special states first
  if (loading) return <p>Loading...</p>;
  if (error) return <p style={{ color: "red" }}>Problem: {error}</p>;
  if (orders.length === 0) return <p>No orders yet</p>;

  return (
    <div>
      {/* ternary */}
      <h2>{user ? `Welcome, ${user.name}` : "Guest"}</h2>

      {/* && : give a true/false condition */}
      {user?.isAdmin && <button>Admin panel</button>}
      {orders.length > 0 && <p>Total {orders.length} orders</p>}

      <ul>
        {orders.map(o => <li key={o.id}>{o.title}</li>)}
      </ul>
    </div>
  );
}

// Many states: lookup object
function StatusBadge({ status }) {
  const map = {
    pending: <span>⏳ Waiting</span>,
    paid: <span>✅ Paid</span>,
    cancelled: <span>❌ Cancelled</span>,
  };
  return map[status] ?? null;
}
```

⚠️ **Common mistakes**

- **`{count && <X />}`.** If `count` is 0, the screen shows `0`. Write `count > 0 && ...`.
- **Tangling up nested ternaries.** For more than two levels, use early returns or a separate component.
- **Calling a Hook inside a condition.** `if (x) { useState() }` is wrong. Call all Hooks **before** an early return.
- **Losing state by removing a component with a condition.** If you need to keep the state, hide it with CSS or lift the state up.

🎯 **Follow-up questions**

- **What happens if you render `false`, `null` or `undefined`?**
  👉 Nothing shows. But `0` and `""` (empty string) are different: `0` is printed.
- **Can you call a Hook before an early return?**
  👉 Yes, you must call all Hooks first. Otherwise the order of Hooks changes.
- **How do you keep many conditions clean?**
  👉 Make small separate components or use a lookup object.

📝 **Remember in one line:** In React, a condition is just plain JavaScript, and beware of `0` with `&&`.

🔮 **Today & future:** Every app needs this for its loading, error, empty and success states.

---

## 4️⃣5️⃣ What is React.memo and when should you use it?

> 🎤 **Full answer:** `React.memo` is a higher-order component. It wraps a component so that it does not render again when its props are the same as in the last render. Normally, when a parent renders, all its children render too, even if their props did not change. `memo` compares each prop with the old one using a shallow compare (`Object.is`). If all match, it reuses the old result. But objects, arrays and functions get a new reference on every render, so when they are props, we must keep them stable with `useMemo` and `useCallback`. We should use `memo` only when a component is heavy and often renders with the same props, and we should measure the problem first with the Profiler.

📖 **Step by step**

- **The problem:** the parent's state changed → the parent renders → all children render, even those that changed nothing.
- **What does `memo` do?**
  👉 Before rendering, it compares new and old props. If all are equal, it skips the render.
- **What shallow compare means**
  👉 Each prop is checked with `===`. `{a:1}` and another `{a:1}` are not equal, because they are different references.
- **The fix for reference problems**
  👉 `useCallback` keeps a function stable. `useMemo` keeps an object, array or value stable.
- **What `memo` cannot stop**
  👉 A change in the component's own state, or a change in a Context it reads.
- **Custom compare**
  👉 `memo(Component, (prev, next) => ...)`. If it returns `true`, the render is skipped. You rarely need it.
- **When to use it**
  👉 Heavy components, rows of a big list, charts. Use it where the parent renders often but the props rarely change.
- **When not to use it**
  👉 On small and light components. The compare also costs time, and the code gets more complex.
- **React Compiler**
  👉 The new compiler can do memoization for you automatically in many cases, so the need to add `memo` by hand is getting smaller.

🧪 **Code**

```jsx
import { memo, useState, useCallback, useMemo } from "react";

// Heavy child: wrapped in memo
const Row = memo(function Row({ item, onRemove }) {
  console.log("Row render:", item.name);
  return (
    <li>
      {item.name}
      <button onClick={() => onRemove(item.id)}>X</button>
    </li>
  );
});

function List() {
  const [items, setItems] = useState([
    { id: 1, name: "Camera" },
    { id: 2, name: "Lens" },
  ]);
  const [dark, setDark] = useState(false);   // unrelated state

  // ❌ Without useCallback: a new function each render, so memo would not work
  // const remove = id => setItems(items.filter(i => i.id !== id));

  // ✅ Stable function (functional update to get the old value)
  const remove = useCallback(
    id => setItems(prev => prev.filter(i => i.id !== id)),
    []
  );

  // ✅ Keep a heavy calculation stable
  const total = useMemo(() => items.length * 100, [items]);

  return (
    <div className={dark ? "dark" : ""}>
      <button onClick={() => setDark(d => !d)}>Change theme</button>
      <p>Total: {total}</p>
      <ul>
        {items.map(i => <Row key={i.id} item={i} onRemove={remove} />)}
      </ul>
    </div>
  );
}
// When you change the theme, Row does not render again (no new text in the console).
```

⚠️ **Common mistakes**

- **Adding `memo` everywhere.** The compare costs time. Often you lose more than you gain.
- **Sending inline functions or objects to a `memo` component.** `onClick={() => ...}` or `style={{...}}` is new each time, so `memo` is useless.
- **Optimizing before measuring.** First use the React DevTools Profiler to see where it is slow.
- **Thinking `memo` also stops renders from Context.** It does not.

🎯 **Follow-up questions**

- **What is the difference between `memo`, `useMemo` and `useCallback`?**
  👉 `memo` wraps a component. `useMemo` remembers a calculated value. `useCallback` remembers the reference of a function.
- **Why does `memo` not work when I pass an object as a prop?**
  👉 A new reference is made on every render, so the shallow compare sees it as different.
- **Does `memo` always stop the render?**
  👉 No. The component still renders when its own state or context changes, or when props really change.

📝 **Remember in one line:** If props do not change, skip the render, but do not forget to keep references stable.

🔮 **Today & future:** The React Compiler will cut down hand-written memoization a lot, but interviewers still ask about the idea.
