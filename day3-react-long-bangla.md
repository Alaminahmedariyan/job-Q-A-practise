# 🔵 React Fundamentals — বিস্তারিত গাইড (বাংলা)

**Day 3 টপিক:** Components, Hooks & State Management

## 📘 এই ফাইল কীভাবে ব্যবহার করবেন

1. **🎤 পূর্ণ উত্তর** পড়ুন, এটা ইন্টারভিউয়ে বলার বড় উত্তর।
2. **📖 ধাপে ধাপে বুঝুন** অংশে বিষয়টা গভীরে বুঝুন।
3. **🧪 কোড** নিজে লিখে চালান। শুধু পড়লে হবে না।
4. **⚠️ সাধারণ ভুল** মন দিয়ে পড়ুন, ইন্টারভিউয়ে এখান থেকেই ফাঁদ প্রশ্ন আসে।
5. **🎯 ফলো-আপ প্রশ্ন** নিজে আগে উত্তর ভাবুন, তারপর নিচেরটা দেখুন।
6. ছোট সংস্করণ চাইলে `day3-react-short-bangla.md` দেখুন।

---

## 3️⃣1️⃣ React কী এবং এটা কোন সমস্যার সমাধান করে?

> 🎤 **পূর্ণ উত্তর:** React হলো Meta-র তৈরি একটি open-source JavaScript library, যা user interface বানাতে ব্যবহার হয়। এর মূল ধারণা হলো UI-কে ছোট ছোট স্বাধীন ও পুনঃব্যবহারযোগ্য অংশে (component) ভাগ করা। React আসার আগে ডেটা বদলালে আমাদের হাতে হাতে `document.getElementById(...)` দিয়ে DOM বদলাতে হতো। অ্যাপ বড় হলে এই কোড জটিল হয়ে যেত, আর ডেটা এবং স্ক্রিন প্রায়ই মিলত না। React-এ আমি শুধু বলি "এই ডেটা হলে UI এমন দেখাবে" (declarative), আর ডেটা বদলালে React নিজেই ঠিক যতটুকু দরকার ততটুকু স্ক্রিন আপডেট করে।

📖 **ধাপে ধাপে বুঝুন**

- **সমস্যা ১: UI আর ডেটা আলাদা হয়ে যাওয়া**
  👉 ডেটা বদলালে স্ক্রিনের কোন কোন জায়গা বদলাতে হবে, তা মনে রাখা কঠিন। একটা জায়গা ভুলে গেলেই বাগ।
- **সমস্যা ২: কোড পুনরায় ব্যবহার করা যেত না**
  👉 একই কার্ড ১০ জায়গায় লাগলে ১০ বার কপি-পেস্ট করতে হতো।
- **সমাধান ১: Declarative UI**
  👉 "কীভাবে" নয়, "কী" লিখি। React ভেতরে হিসাব করে।
- **সমাধান ২: Component**
  👉 একবার বানাও, বারবার ব্যবহার করো। বদলাতে হলে এক জায়গায় বদলালেই সব জায়গায় বদলায়।
- **সমাধান ৩: Virtual DOM**
  👉 React পুরো পাতা না এঁকে শুধু বদলানো অংশ আপডেট করে।
- **সমাধান ৪: One-way data flow**
  👉 ডেটা parent থেকে child-এ নামে। কোথা থেকে কী এল খুঁজে পাওয়া সহজ।

🧪 **কোড**

```jsx
// Imperative (পুরনো ধরন): হাতে হাতে DOM বদলানো
const p = document.getElementById("count");
p.textContent = Number(p.textContent) + 1;

// Declarative (React): শুধু বলি UI ডেটার উপর নির্ভর করে
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

⚠️ **সাধারণ ভুল**

- **React-কে framework বলা।** React একটা library। Routing, SSR ইত্যাদির জন্য Next.js-এর মতো framework লাগে।
- **"React মানেই দ্রুত" ভাবা।** React দ্রুত হওয়ার চেয়ে বেশি কাজ করে কোড গোছানো ও রক্ষণাবেক্ষণ সহজ করতে।

🎯 **ফলো-আপ প্রশ্ন**

- **Library আর framework-এর পার্থক্য কী?**
  👉 Library-কে আমরা ডাকি (আমরা নিয়ন্ত্রণ করি)। Framework আমাদের কোডকে ডাকে (সে নিয়ন্ত্রণ করে)। React শুধু UI-র কাজ দেয়, বাকি সিদ্ধান্ত আমাদের।
- **Declarative আর imperative-এর পার্থক্য?**
  👉 Imperative = ধাপে ধাপে নির্দেশ ("এটা করো, তারপর ওটা")। Declarative = ফলাফল বর্ণনা ("এমন দেখতে চাই")।

📝 **এক লাইনে মনে রাখুন:** ডেটা বদলাও, React স্ক্রিন বদলাবে।

🔮 **আজ ও ভবিষ্যতে:** Next.js, React Native, Remix সবকিছুর ভিত্তি React।

---

## 3️⃣2️⃣ JSX কী এবং React-এ কেন ব্যবহার হয়?

> 🎤 **পূর্ণ উত্তর:** JSX (JavaScript XML) হলো JavaScript-এর একটি সিনট্যাক্স এক্সটেনশন, যাতে JavaScript ফাইলের ভেতরেই HTML-এর মতো করে UI লেখা যায়। ব্রাউজার JSX বোঝে না, তাই Babel বা SWC-এর মতো কম্পাইলার এটাকে সাধারণ JavaScript function call-এ রূপান্তর করে। আমরা JSX ব্যবহার করি কারণ UI-র গঠন আর তার লজিক একই component-এ থাকে, ফলে পড়তে ও বুঝতে সুবিধা হয়। JSX ছাড়াও React লেখা সম্ভব, কিন্তু কোড অনেক লম্বা ও কঠিন হতো।

📖 **ধাপে ধাপে বুঝুন**

- **ধাপ ১: আপনি JSX লেখেন**
  👉 `<h1 className="title">Hi</h1>`
- **ধাপ ২: কম্পাইলার এটাকে JavaScript-এ বদলায়**
  👉 `React.createElement("h1", { className: "title" }, "Hi")` ধরনের কোড (নতুন সংস্করণে `jsx()` function)।
- **ধাপ ৩: এটা একটা সাধারণ object ফেরত দেয়**
  👉 এই object-ই Virtual DOM-এর একটা অংশ।
- **JSX-এর নিয়মগুলো**
  👉 একটাই root, সব tag বন্ধ, `className`, `htmlFor`, camelCase attribute (`onClick`, `tabIndex`)।
- **`{ }`-এর ভেতরে শুধু expression**
  👉 `{a + b}`, `{cond ? x : y}`, `{list.map(...)}` চলে। `if`, `for`, `const` চলে না।
- **Style দিতে object লাগে**
  👉 `style={{ color: "red", fontSize: 20 }}`। বাইরের `{}` JavaScript, ভেতরের `{}` object।

🧪 **কোড**

```jsx
function Profile() {
  const user = { name: "Alamin", skills: ["JS", "React"] };

  return (
    // একাধিক element-কে Fragment দিয়ে মোড়ানো
    <>
      <h1 className="title" style={{ color: "teal" }}>
        {user.name}
      </h1>

      <label htmlFor="email">ইমেইল</label>
      <input id="email" type="email" />

      <ul>
        {user.skills.map(s => <li key={s}>{s}</li>)}
      </ul>
    </>
  );
}
```

⚠️ **সাধারণ ভুল**

- **`class` লেখা।** JSX-এ `className` লিখতে হয়।
- **Tag বন্ধ না করা।** `<input>` নয়, `<input />`।
- **`{}`-এর ভেতরে `if` লেখা।** এটা statement, expression নয়। ternary বা `&&` ব্যবহার করুন।
- **Object সরাসরি রেন্ডার করা।** `{user}` লিখলে error হয়। `{user.name}` লিখুন।

🎯 **ফলো-আপ প্রশ্ন**

- **JSX কি বাধ্যতামূলক?**
  👉 না। `React.createElement` দিয়েও লেখা যায়, কিন্তু কেউ তা করে না।
- **Fragment কেন লাগে?**
  👉 বাড়তি `<div>` না বানিয়ে একাধিক element ফেরত দিতে।
- **JSX-এ XSS থেকে কি নিরাপত্তা আছে?**
  👉 হ্যাঁ, `{ }` দিয়ে বসানো মান React স্বয়ংক্রিয়ভাবে escape করে। কিন্তু `dangerouslySetInnerHTML` ব্যবহার করলে সেই নিরাপত্তা থাকে না।

📝 **এক লাইনে মনে রাখুন:** JSX দেখতে HTML, আসলে JavaScript।

🔮 **আজ ও ভবিষ্যতে:** TypeScript-এর সাথে TSX, আর server component-এও একই সিনট্যাক্স।

---

## 3️⃣3️⃣ Functional ও Class component-এর পার্থক্য কী?

> 🎤 **পূর্ণ উত্তর:** Functional component হলো একটি সাধারণ JavaScript function, যা props নেয় এবং JSX ফেরত দেয়। React 16.8 থেকে Hooks আসার পর functional component-এও state, lifecycle ও অন্য সব সুবিধা পাওয়া যায়। Class component `React.Component` থেকে extend করে, `render()` method লাগে এবং state রাখে `this.state`-এ। এখন সবাই functional component লেখে কারণ কোড ছোট, `this`-এর ঝামেলা নেই, আর লজিক আলাদা করে পুনরায় ব্যবহার করা যায় (custom hook)। তবে error boundary এখনও class দিয়েই বানাতে হয়, আর পুরনো প্রজেক্টে class কোড দেখা যায়।

📖 **ধাপে ধাপে বুঝুন**

- **State রাখা**
  👉 Functional: `useState`। Class: `this.state` ও `this.setState`।
- **Lifecycle**
  👉 Class-এ আলাদা আলাদা method (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`)। Functional-এ সবকিছু `useEffect` দিয়ে।
- **`this`-এর সমস্যা**
  👉 Class-এ event handler-এ `this` হারিয়ে যায়, তাই `bind` বা arrow function লাগে।
- **লজিক পুনরায় ব্যবহার**
  👉 Class-এ HOC বা render props লাগত, যা জটিল। Functional-এ custom hook দিয়ে সহজেই হয়।
- **ছোট কোড**
  👉 একই কাজ functional-এ প্রায় অর্ধেক লাইনে হয়।

| বৈশিষ্ট্য | Functional | Class |
|---|---|---|
| লেখা | function | `class ... extends React.Component` |
| State | `useState` | `this.state` |
| Lifecycle | `useEffect` | আলাদা আলাদা method |
| `this` | লাগে না | লাগে |
| লজিক শেয়ার | custom hook | HOC / render props |
| Error Boundary | বানানো যায় না | বানানো যায় |
| বর্তমান পছন্দ | ✅ | পুরনো কোডে |

🧪 **কোড**

```jsx
// Functional: ডেটা আনা + state
function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("/api/users").then(r => r.json()).then(setUsers);
  }, []);

  return <p>{users.length} জন</p>;
}

// Class: একই কাজ
class UsersC extends React.Component {
  state = { users: [] };

  componentDidMount() {
    fetch("/api/users").then(r => r.json()).then(users => this.setState({ users }));
  }

  render() {
    return <p>{this.state.users.length} জন</p>;
  }
}
```

⚠️ **সাধারণ ভুল**

- **"Functional-এ state নেই" বলা।** এটা Hooks-এর আগের কথা। এখন আছে।
- **Class-এ method bind করতে ভোলা।** `this.setState` তখন কাজ করে না।

🎯 **ফলো-আপ প্রশ্ন**

- **Class component কি বন্ধ হয়ে যাবে?**
  👉 না, React এখনও সাপোর্ট করে। কিন্তু নতুন কোডে ব্যবহার করার পরামর্শ নেই।
- **`useEffect` কি lifecycle method-এর সরাসরি বদলি?**
  👉 ঠিক নয়। এটা "সিঙ্ক্রোনাইজেশন" ধারণা: state-এর সাথে বাইরের জগৎ মিলিয়ে রাখা।

📝 **এক লাইনে মনে রাখুন:** নতুন কোড = functional + Hooks।

🔮 **আজ ও ভবিষ্যতে:** পুরনো প্রজেক্টে কাজ পেলে class বোঝা লাগবে।

---

## 3️⃣4️⃣ Virtual DOM কী এবং React এটা কীভাবে ব্যবহার করে?

> 🎤 **পূর্ণ উত্তর:** Virtual DOM হলো আসল DOM-এর একটা হালকা JavaScript object প্রতিরূপ, যা মেমরিতে থাকে। State বা props বদলালে React নতুন একটা Virtual DOM tree বানায় এবং আগেরটার সাথে তুলনা করে। এই তুলনাকে diffing বলে। তুলনায় যা যা বদলেছে, React শুধু সেগুলো একসাথে (batch করে) আসল DOM-এ প্রয়োগ করে। পুরো প্রক্রিয়ার নাম reconciliation। এতে আমরা সরাসরি DOM না ছুঁয়েও দক্ষভাবে UI আপডেট করতে পারি।

📖 **ধাপে ধাপে বুঝুন**

- **ধাপ ১: Render**
  👉 Component চলে এবং JSX থেকে React element-এর tree (Virtual DOM) তৈরি হয়।
- **ধাপ ২: Diff**
  👉 নতুন tree আর পুরনো tree তুলনা হয়।
- **ধাপ ৩: Commit**
  👉 শুধু তফাতগুলো আসল DOM-এ প্রয়োগ হয়।
- **Diffing-এর দুটো মূল নিয়ম**
  👉 (১) element-এর type আলাদা হলে (যেমন `div` থেকে `span`) পুরো subtree নতুন করে বানায়। (২) list-এ `key` দেখে বোঝে কোন item কোনটা।
- **Batching**
  👉 একাধিক state আপডেট একসাথে করে একবারই render হয়।
- **Fiber**
  👉 React-এর ভেতরের নতুন ইঞ্জিন, যা কাজকে ছোট ছোট টুকরোয় ভাগ করে ব্রাউজারকে আটকে না রেখে চালাতে পারে।

🧪 **কোড**

```jsx
function App() {
  const [count, setCount] = useState(0);
  console.log("App render হলো");

  return (
    <div>
      <h1>Static title</h1>        {/* বদলায়নি → DOM ছোঁয়া হয় না */}
      <p>Count: {count}</p>        {/* বদলেছে → শুধু এই লেখা আপডেট */}
      <button onClick={() => setCount(c => c + 1)}>+</button>
    </div>
  );
}
// DevTools-এ Elements ট্যাব খুলে দেখুন: বোতাম চাপলে শুধু <p>-এর লেখা ঝলকাবে।
```

⚠️ **সাধারণ ভুল**

- **"Virtual DOM আসল DOM-এর চেয়ে দ্রুত" বলা।** আসলে এটা অতিরিক্ত কাজ করে। সুবিধা হলো আমাদের নিজে DOM বদলানোর ঝামেলা নেই এবং React বুদ্ধি করে কম বদলায়।
- **Virtual DOM আর Shadow DOM গুলিয়ে ফেলা।** Shadow DOM হলো ব্রাউজারের ফিচার (CSS আলাদা রাখা), Virtual DOM হলো React-এর কৌশল।

🎯 **ফলো-আপ প্রশ্ন**

- **Reconciliation কী?**
  👉 পুরনো ও নতুন Virtual DOM তুলনা করে কী বদলাতে হবে ঠিক করার প্রক্রিয়া।
- **কেন key দরকার?**
  👉 list-এর item চিনতে, যাতে অযথা সব item নতুন করে বানাতে না হয়।

📝 **এক লাইনে মনে রাখুন:** তুলনা করো, শুধু তফাতটুকু আপডেট করো।

🔮 **আজ ও ভবিষ্যতে:** performance সমস্যা বুঝতে (কেন বারবার render হচ্ছে) এই ধারণা কাজে লাগে।

---

## 3️⃣5️⃣ useState hook উদাহরণসহ ব্যাখ্যা করুন।

> 🎤 **পূর্ণ উত্তর:** `useState` হলো React-এর একটি Hook, যা functional component-কে নিজস্ব state রাখার ক্ষমতা দেয়। `const [value, setValue] = useState(initial)` লিখলে দুটো জিনিস পাই: বর্তমান মান এবং সেটা বদলানোর function। Setter ডাকলে React নতুন মান সংরক্ষণ করে এবং component আবার render করে, ফলে UI আপডেট হয়। State সরাসরি বদলানো যায় না, কারণ তাহলে React পরিবর্তন টের পায় না। Object বা array বদলাতে হলে সবসময় নতুন কপি বানিয়ে দিতে হয়, আর আগের মানের উপর নির্ভর করলে `setX(prev => ...)` রূপ ব্যবহার করতে হয়।

📖 **ধাপে ধাপে বুঝুন**

- **প্রথম render:** `useState(0)` থেকে শুরুর মান 0 নেয়।
- **পরের render:** React আগের সংরক্ষিত মানই দেয়, শুরুর মান আর ব্যবহার করে না।
- **Setter ডাকলে:** React render-এর সারিতে কাজ রাখে, তারপর নতুন মান নিয়ে component আবার চালায়।
- **Snapshot ধারণা**
  👉 প্রতিটা render-এ state একটা "ছবি"-র মতো স্থির। একই render-এর ভেতরে `count` বদলায় না, সেজন্য `setCount(count + 1)` তিনবার লিখলেও মাত্র ১ বাড়ে।
- **Functional update**
  👉 `setCount(c => c + 1)` তিনবার লিখলে ৩ বাড়ে, কারণ প্রতিটা সর্বশেষ মান থেকে শুরু করে।
- **Lazy initial state**
  👉 ভারী হিসাব হলে `useState(() => heavyWork())`। এতে শুধু প্রথমবার চলে।
- **Object/array: immutable আপডেট**
  👉 `{ ...obj, key: new }`, `[...arr, item]`, `arr.filter(...)`, `arr.map(...)`।

🧪 **কোড**

```jsx
import { useState } from "react";

function Demo() {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([]);
  const [form, setForm] = useState({ name: "", age: 0 });

  const addThree = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);          // মাত্র +1 (সবাই একই পুরনো count দেখে)
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
      <button onClick={addThree}>ভুল</button>
      <button onClick={addThreeRight}>ঠিক</button>
    </div>
  );
}
```

⚠️ **সাধারণ ভুল**

- **State সরাসরি বদলানো।** `todos.push(x)` বা `form.name = "A"` করলে UI আপডেট হয় না।
- **Setter-এর পরেই নতুন মান পড়ার আশা।** `setCount(5); console.log(count);` পুরনো মান দেখাবে।
- **Derived ডেটা আলাদা state-এ রাখা।** `fullName` সরাসরি `first + last` থেকে হিসাব করুন, আলাদা state বানাবেন না।
- **Hook শর্তের ভেতরে বা loop-এ ডাকা।** Hook সবসময় component-এর একদম উপরের স্তরে ডাকতে হয়।

🎯 **ফলো-আপ প্রশ্ন**

- **একই মান সেট করলে কি re-render হয়?**
  👉 React `Object.is` দিয়ে তুলনা করে, মান একই হলে সাধারণত render এড়িয়ে যায়।
- **State কি async?**
  👉 Setter নিজে কিছু ফেরত দেয় না, আর আপডেট batch হয়। তাই নতুন মান পরের render-এ পাওয়া যায়।
- **`useState` নাকি `useReducer`?**
  👉 সহজ মান হলে `useState`। অনেকগুলো সম্পর্কিত state বা জটিল আপডেট নিয়ম হলে `useReducer`।

📝 **এক লাইনে মনে রাখুন:** state নিজে বদলাবেন না, setter দিয়ে নতুন কপি দিন।

🔮 **আজ ও ভবিষ্যতে:** form, modal, filter, toggle: সব interactive UI-র ভিত্তি।

---

## 3️⃣6️⃣ useEffect hook কী এবং এর ব্যবহার কী কী?

> 🎤 **পূর্ণ উত্তর:** `useEffect` হলো এমন একটি Hook, যা দিয়ে component render হওয়ার পরে side effect চালানো যায়। Side effect মানে render-এর বাইরের কাজ: API থেকে ডেটা আনা, timer বা subscription চালানো, event listener বসানো, `document.title` বদলানো ইত্যাদি। দ্বিতীয় argument dependency array ঠিক করে effect কখন চলবে। Effect থেকে একটি cleanup function ফেরত দিলে সেটা component মুছে যাওয়ার আগে বা পরের effect চলার আগে চলে, যাতে memory leak না হয়।

📖 **ধাপে ধাপে বুঝুন**

- **কখন চলে?**
  👉 React স্ক্রিন আঁকার পরে।
- **Dependency array-এর তিন রূপ**
  👉 (১) না দিলে প্রতি render-এ। (২) `[]` হলে শুধু প্রথমবার। (৩) `[x, y]` হলে প্রথমবার এবং x বা y বদলালে।
- **Cleanup কখন চলে?**
  👉 পরের effect চলার আগে, এবং component মুছে যাওয়ার সময়।
- **Stale closure**
  👉 Effect-এর ভেতরে যে state/props ব্যবহার করবেন সেগুলো dependency-তে দিতে হবে, নইলে পুরনো মান আটকে থাকতে পারে।
- **Race condition**
  👉 দ্রুত ID বদলালে পুরনো request পরে ফিরে এসে নতুন ডেটা ঢেকে দিতে পারে। এড়াতে cleanup-এ flag বা `AbortController` ব্যবহার করুন।
- **Strict Mode**
  👉 Dev-এ effect দুবার চলে। এটা আপনার cleanup ঠিক আছে কি না যাচাই করার জন্য।
- **কখন useEffect লাগে না**
  👉 render থেকেই হিসাব করা যায় এমন মান, বা বোতাম চাপার প্রতিক্রিয়া (এগুলো event handler-এ হবে)।

🧪 **কোড**

```jsx
import { useState, useEffect } from "react";

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // ১) ডেটা আনা (userId বদলালে আবার), race condition সামলে
  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);

    fetch(`/api/users/${userId}`, { signal: controller.signal })
      .then(r => r.json())
      .then(data => { setUser(data); setLoading(false); })
      .catch(err => { if (err.name !== "AbortError") console.error(err); });

    return () => controller.abort();   // পুরনো request বাতিল
  }, [userId]);

  // ২) event listener + cleanup
  useEffect(() => {
    const onResize = () => console.log(window.innerWidth);
    window.addEventListener("resize", onResize);
    return () => window.removeEventListener("resize", onResize);
  }, []);

  // ৩) document title
  useEffect(() => {
    if (user) document.title = user.name;
  }, [user]);

  if (loading) return <p>লোড হচ্ছে...</p>;
  return <h2>{user.name}</h2>;
}
```

⚠️ **সাধারণ ভুল**

- **Dependency array ভুলে যাওয়া।** `useEffect(() => { setX(...) })` লিখলে অসীম লুপ হতে পারে।
- **Cleanup না দেওয়া।** timer বা listener থেকে যায়, memory leak হয়।
- **Dependency ফাঁকি দেওয়া।** `// eslint-disable` দিয়ে লুকালে পুরনো মানের বাগ আসে।
- **`async` function সরাসরি effect-এ দেওয়া।** `useEffect(async () => ...)` ভুল, কারণ effect cleanup function ফেরত দিতে পারে, Promise নয়। ভেতরে আলাদা async function বানিয়ে ডাকুন।

🎯 **ফলো-আপ প্রশ্ন**

- **`useEffect` আর `useLayoutEffect`-এর পার্থক্য?**
  👉 `useLayoutEffect` স্ক্রিন আঁকার আগেই চলে (DOM মাপার জন্য), আর `useEffect` পরে চলে।
- **ডেটা আনার জন্য কি useEffect-ই সেরা?**
  👉 না। TanStack Query, SWR বা Next.js server component-এ cache, retry, loading অবস্থা নিজে থেকে মেলে।
- **Effect দুবার চলছে কেন?**
  👉 Strict Mode, শুধু development-এ।

📝 **এক লাইনে মনে রাখুন:** useEffect = বাইরের জগতের সাথে সিঙ্ক রাখা, আর cleanup ভুলবেন না।

🔮 **আজ ও ভবিষ্যতে:** আধুনিক অ্যাপে এর ব্যবহার কমছে, কিন্তু বুঝে ব্যবহার করা জরুরি।

---

## 3️⃣7️⃣ Controlled ও Uncontrolled component-এর পার্থক্য কী?

> 🎤 **পূর্ণ উত্তর:** Controlled component-এ form element-এর (input, textarea, select) মান React state-এ থাকে। আমরা `value` prop দিয়ে মান দেখাই এবং `onChange` দিয়ে প্রতিটা পরিবর্তন state-এ লিখি, তাই React-ই একমাত্র সত্যের উৎস। Uncontrolled component-এ মান থাকে ব্রাউজারের DOM-এ। আমরা `defaultValue` দিয়ে শুরুর মান দিই এবং দরকারের সময় `ref` দিয়ে পড়ি। Controlled-এ লাইভ validation, মান ফরম্যাট করা, বোতাম বন্ধ/চালু করা সহজ। Uncontrolled-এ কোড কম ও সহজ, আর file input সবসময় uncontrolled।

📖 **ধাপে ধাপে বুঝুন**

- **Controlled-এর চক্র**
  👉 ব্যবহারকারী টাইপ করে → `onChange` চলে → state বদলায় → React আবার render করে → input নতুন মান দেখায়।
- **Uncontrolled-এর চক্র**
  👉 ব্যবহারকারী টাইপ করে → ব্রাউজার নিজেই মান রাখে → React কিছু জানে না → জমা দেওয়ার সময় `ref.current.value` পড়ি।
- **`value` vs `defaultValue`**
  👉 `value` = React নিয়ন্ত্রণ করে (controlled)। `defaultValue` = শুধু শুরুর মান (uncontrolled)।
- **কখন কোনটা**
  👉 লাইভ validation, কয়েকটি field একে অপরের উপর নির্ভরশীল, বা মান ফরম্যাট করতে হলে controlled। ছোট সহজ form বা file upload হলে uncontrolled।
- **Performance**
  👉 Controlled-এ প্রতি অক্ষরে re-render হয়। বড় form-এ React Hook Form (uncontrolled ধরনের) এই সমস্যা কমায়।
- **Controlled ↔ uncontrolled বদলানো ঠিক নয়**
  👉 `value` প্রথমে `undefined` ছিল, পরে মান পেলে React সতর্কতা দেয়। শুরুতেই `""` দিন।

🧪 **কোড**

```jsx
import { useState, useRef } from "react";

// Controlled: লাইভ validation সহ
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
      <input value={email} onChange={e => setEmail(e.target.value)} placeholder="ইমেইল" />
      <input type="password" value={password}
             onChange={e => setPassword(e.target.value)} placeholder="পাসওয়ার্ড" />
      {!valid && <p>ইমেইলে @ এবং পাসওয়ার্ড ৬+ অক্ষর লাগবে</p>}
      <button disabled={!valid}>জমা দিন</button>
    </form>
  );
}

// Uncontrolled: ref দিয়ে পড়া
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
      <button>জমা দিন</button>
    </form>
  );
}
```

⚠️ **সাধারণ ভুল**

- **`value` দিয়ে `onChange` না দেওয়া।** input আটকে যায়, টাইপ করা যায় না।
- **Checkbox-এ `value`-র বদলে `checked` না দেওয়া।** checkbox-এ `checked` ও `onChange` লাগে।
- **`e.preventDefault()` ভুলে যাওয়া।** form জমা দিলে পাতা রিলোড হয়ে যায়।

🎯 **ফলো-আপ প্রশ্ন**

- **Controlled component-এ কি সবসময় `useState` লাগে?**
  👉 মান React-এর কোনো state বা বাইরের store থেকে আসতে হবে, `useState` সবচেয়ে সাধারণ উপায়।
- **File input কেন uncontrolled?**
  👉 নিরাপত্তার কারণে ব্রাউজার কোড দিয়ে file input-এর মান সেট করতে দেয় না।

📝 **এক লাইনে মনে রাখুন:** Controlled = React মান ধরে রাখে। Uncontrolled = DOM ধরে রাখে।

🔮 **আজ ও ভবিষ্যতে:** React Hook Form + Zod প্রায় স্ট্যান্ডার্ড জুটি হয়ে গেছে।

---

## 3️⃣8️⃣ React-এ props কী এবং কীভাবে পাঠানো হয়?

> 🎤 **পূর্ণ উত্তর:** Props (properties) হলো parent component থেকে child component-কে পাঠানো ইনপুট ডেটা। JSX-এ HTML attribute-এর মতো লিখে পাঠানো হয় এবং child সেগুলো একটি object হিসেবে পায়। Props read-only, অর্থাৎ child সেগুলো বদলাতে পারে না, কারণ ডেটা একমুখী (উপর থেকে নিচে) প্রবাহিত হয়। String, number, object, array, function, এমনকি JSX-ও props হিসেবে পাঠানো যায়। Function পাঠিয়ে child থেকে parent-কে ঘটনা জানানো যায়। `children` হলো বিশেষ prop, যা ট্যাগের ভেতরের কনটেন্ট ধরে।

📖 **ধাপে ধাপে বুঝুন**

- **ধাপ ১: পাঠানো**
  👉 `<Card title="Hi" price={500} />`। String হলে `""`, বাকি সব `{}`।
- **ধাপ ২: নেওয়া**
  👉 `function Card(props)` অথবা destructuring `function Card({ title, price })`।
- **Default মান**
  👉 `({ price = 0 })`। শুধু `undefined` হলে কাজ করে।
- **Spread দিয়ে পাঠানো**
  👉 `<Card {...data} />` মানে object-এর সব key prop হয়ে যায়।
- **Function পাঠানো (callback prop)**
  👉 `onDelete={() => remove(id)}`। child ডাকলে parent-এর কোড চলে।
- **`children`**
  👉 `<Modal><p>ভেতরের কনটেন্ট</p></Modal>`। layout component বানাতে খুব কাজের।
- **Props বদলালে re-render**
  👉 parent নতুন props দিলে child আবার render হয়।
- **Props পরিবর্তন করা নিষিদ্ধ**
  👉 `props.name = "X"` করা যায় না। বদলাতে হলে parent-এর state বদলাতে হবে।

🧪 **কোড**

```jsx
// Child: destructuring + default + callback + children
function ProductCard({ name, price = 0, inStock = true, onBuy, children }) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>{price} টাকা {inStock ? "" : "(শেষ)"}</p>
      {children}
      <button disabled={!inStock} onClick={() => onBuy(name)}>কিনুন</button>
    </div>
  );
}

// Parent
function Shop() {
  const [cart, setCart] = useState([]);
  const products = [
    { id: 1, name: "ক্যামেরা", price: 500, inStock: true },
    { id: 2, name: "ট্রাইপড", price: 200, inStock: false },
  ];

  return (
    <div>
      {products.map(p => (
        <ProductCard key={p.id} {...p} onBuy={n => setCart([...cart, n])}>
          <small>৩ দিনের ভাড়া</small>
        </ProductCard>
      ))}
      <p>কার্টে: {cart.length}টি</p>
    </div>
  );
}
```

⚠️ **সাধারণ ভুল**

- **Props বদলানোর চেষ্টা।** এটা React-এর নিয়মের বিরুদ্ধে।
- **Props থেকে state কপি করা।** `useState(props.value)` শুধু প্রথমবার মান নেয়, পরে props বদলালে state বদলায় না। সরাসরি props ব্যবহার করুন বা `key` বদলে component রিসেট করুন।
- **Function call করে পাঠানো।** `onClick={handle()}` ভুল (সাথে সাথে চলে যায়), `onClick={handle}` বা `onClick={() => handle(x)}` ঠিক।
- **Number-কে string হিসেবে পাঠানো।** `price="500"` আর `price={500}` এক নয়।

🎯 **ফলো-আপ প্রশ্ন**

- **Props কি যেকোনো type-এর হতে পারে?**
  👉 হ্যাঁ, function ও JSX-ও।
- **কীভাবে props-এর type যাচাই করবেন?**
  👉 TypeScript (প্রচলিত), বা পুরনো `PropTypes`।
- **Child থেকে parent-কে ডেটা কীভাবে পাঠাবেন?**
  👉 Parent থেকে callback function props হিসেবে পাঠিয়ে child সেটা ডাকবে ডেটা সহ।

📝 **এক লাইনে মনে রাখুন:** Props নিচে নামে, ঘটনা (callback) উপরে ওঠে।

🔮 **আজ ও ভবিষ্যতে:** component library (shadcn/ui, MUI) সবই props-এর উপর দাঁড়িয়ে।

---

## 3️⃣9️⃣ Prop drilling কী এবং কীভাবে এড়ানো যায়?

> 🎤 **পূর্ণ উত্তর:** Prop drilling হলো একটা ডেটা অনেক স্তর নিচের component-এ পৌঁছানোর জন্য মাঝের প্রতিটি component দিয়ে props পার করানো, যদিও মাঝের component-গুলোর ওই ডেটার নিজের কোনো দরকার নেই। এতে মাঝের component-গুলো অযথা জটিল হয়, ডেটার নাম বদলালে অনেক ফাইল বদলাতে হয়, আর কোড বোঝা কঠিন হয়। এড়ানোর প্রধান উপায় তিনটি: Context API, component composition (`children` বা JSX prop) এবং Zustand বা Redux-এর মতো state management library।

📖 **ধাপে ধাপে বুঝুন**

- **উদাহরণ:** `App → Dashboard → Sidebar → UserMenu → Avatar`
  👉 শুধু Avatar-এর `user` লাগে, কিন্তু Dashboard, Sidebar, UserMenu সবাইকে `user` ধরে পাঠাতে হয়।
- **সমাধান ১: Context API**
  👉 উপরে `UserContext.Provider`-এ `user` রাখুন। Avatar সরাসরি `useContext` দিয়ে নেয়। মাঝের কেউ কিছু জানে না।
- **সমাধান ২: Composition**
  👉 `<Dashboard avatar={<Avatar user={user} />} />`। Avatar আগেই তৈরি হয়ে উপরেই `user` পেয়ে গেছে, মাঝে পাঠানোর দরকার নেই।
- **সমাধান ৩: State library**
  👉 Zustand-এ `const user = useStore(s => s.user)` লিখে যেকোনো জায়গা থেকে নেওয়া যায়।
- **সমাধান ৪: Custom hook**
  👉 `useUser()` hook বানিয়ে ভেতরে Context বা store লুকানো।
- **কখন drilling ঠিক আছে**
  👉 ১-২ স্তর হলে। অতিরিক্ত Context বানানো অপ্রয়োজনীয় জটিলতা।

🧪 **কোড**

```jsx
// ❌ Prop drilling
function App() { const user = { name: "Alamin" }; return <Dashboard user={user} />; }
function Dashboard({ user }) { return <Sidebar user={user} />; }
function Sidebar({ user }) { return <Avatar user={user} />; }
function Avatar({ user }) { return <span>{user.name}</span>; }

// ✅ সমাধান ১: Context
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

// ✅ সমাধান ২: Composition
function App2() {
  const user = { name: "Alamin" };
  return <Dashboard avatar={<Avatar2 user={user} />} />;
}
function Dashboard({ avatar }) { return <aside>{avatar}</aside>; }
function Avatar2({ user }) { return <span>{user.name}</span>; }
```

⚠️ **সাধারণ ভুল**

- **সবকিছুর জন্য Context বানানো।** Context বদলালে সব consumer re-render হয়, অনেক Context মেইনটেইন করাও কঠিন।
- **Context-এ ঘন ঘন বদলানো ডেটা রাখা।** performance খারাপ হয়।
- **"Context = state management" ভাবা।** Context শুধু ডেটা পৌঁছানোর পথ। State রাখে `useState`/`useReducer`।

🎯 **ফলো-আপ প্রশ্ন**

- **Context-এর অসুবিধা কী?**
  👉 Value বদলালে সব consumer render হয়। বড় অ্যাপে Zustand/Redux সূক্ষ্মভাবে নিয়ন্ত্রণ দেয়।
- **Composition কীভাবে drilling কমায়?**
  👉 মাঝের component-গুলো ডেটার বদলে তৈরি JSX নেয়, ফলে ডেটা বহন করতে হয় না।

📝 **এক লাইনে মনে রাখুন:** যার ডেটা লাগে সে-ই সরাসরি নেবে, মাঝের কেউ ডাকপিয়ন নয়।

🔮 **আজ ও ভবিষ্যতে:** auth, theme, cart, ভাষা, এগুলো সাধারণত Context বা Zustand-এ রাখা হয়।

---

## 4️⃣0️⃣ useContext hook উদাহরণসহ ব্যাখ্যা করুন।

> 🎤 **পূর্ণ উত্তর:** `useContext` Hook দিয়ে একটি component কাছের উপরের Provider থেকে ভাগ করা ডেটা সরাসরি পড়তে পারে, মাঝের স্তরে props না পাঠিয়ে। তিন ধাপে ব্যবহার হয়: প্রথমে `createContext` দিয়ে context বানাই, তারপর উপরে `Context.Provider`-এর `value`-তে ডেটা দিই, আর নিচের যেকোনো component-এ `useContext(Context)` দিয়ে সেই মান নিই। Provider-এর `value` বদলালে সব consumer component আবার render হয়। তাই theme, logged-in user, ভাষা-র মতো কম বদলানো গ্লোবাল ডেটার জন্য এটা ভালো, কিন্তু ঘন ঘন বদলানো ডেটার জন্য নয়।

📖 **ধাপে ধাপে বুঝুন**

- **ধাপ ১: context তৈরি**
  👉 `const AuthContext = createContext(null);`
- **ধাপ ২: Provider component বানানো**
  👉 state ও লজিক এক জায়গায় রেখে `value`-তে দেওয়া। সাধারণত `AuthProvider` নামে আলাদা component।
- **ধাপ ৩: custom hook বানানো**
  👉 `useAuth()` hook-এ `useContext` লুকানো, সাথে Provider-এর বাইরে ব্যবহার হলে error।
- **ধাপ ৪: ব্যবহার**
  👉 `const { user, login } = useAuth();`
- **Re-render কীভাবে কাজ করে**
  👉 `value` বদলালে সব consumer render হয়। `value`-তে প্রতিবার নতুন object বানালে (`value={{...}}`) অকারণে সবাই render হয়, তাই `useMemo` দিয়ে স্থির রাখা ভালো।
- **একাধিক Context আলাদা রাখা**
  👉 theme আর auth আলাদা Context-এ রাখুন, যাতে একটা বদলালে অন্যের consumer render না হয়।

🧪 **কোড**

```jsx
import { createContext, useContext, useState, useMemo } from "react";

// ১) context
const AuthContext = createContext(null);

// ২) Provider
export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = name => setUser({ name });
  const logout = () => setUser(null);

  // value স্থির রাখা, অকারণ re-render এড়াতে
  const value = useMemo(() => ({ user, login, logout }), [user]);

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}

// ৩) custom hook
export function useAuth() {
  const ctx = useContext(AuthContext);
  if (!ctx) throw new Error("useAuth শুধু AuthProvider-এর ভেতরে ব্যবহার করুন");
  return ctx;
}

// ৪) ব্যবহার
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
    <button onClick={logout}>{user.name}, লগআউট</button>
  ) : (
    <button onClick={() => login("Alamin")}>লগইন</button>
  );
}
```

⚠️ **সাধারণ ভুল**

- **Provider-এর বাইরে `useContext` ডাকা।** শুধু ডিফল্ট মান (বা `null`) পাওয়া যায়, তাই কোড ভাঙে।
- **প্রতি render-এ নতুন `value` object দেওয়া।** সব consumer অযথা render হয়।
- **একটা বিশাল Context-এ সবকিছু রাখা।** ছোট ছোট আলাদা Context ভালো।
- **Context-কে `useState`-এর বিকল্প ভাবা।** শুধু একটা component-এর state হলে Context লাগে না।

🎯 **ফলো-আপ প্রশ্ন**

- **Context আর Redux-এর পার্থক্য?**
  👉 Context ডেটা পৌঁছানোর পথ। Redux পূর্ণাঙ্গ state management (store, action, devtools, middleware)।
- **Consumer কীভাবে অযথা render এড়াবেন?**
  👉 Context ভাগ করা, `useMemo` দিয়ে value স্থির রাখা, বা selector-সমৃদ্ধ library (Zustand)।
- **Next.js App Router-এ Context কোথায় রাখবেন?**
  👉 Provider-কে `"use client"` চিহ্নিত আলাদা client component-এ রাখতে হয়।

📝 **এক লাইনে মনে রাখুন:** create → provide → use।

🔮 **আজ ও ভবিষ্যতে:** প্রায় প্রতিটি অ্যাপে অন্তত একটি `ThemeProvider` বা `AuthProvider` থাকে।

---

## 4️⃣1️⃣ useRef hook কী এবং কখন ব্যবহার করবেন?

> 🎤 **পূর্ণ উত্তর:** `useRef` একটি Hook, যা `{ current: initialValue }` আকারের একটি object ফেরত দেয়। এই object প্রতিটি render-এর মধ্যে একই থাকে এবং `ref.current` বদলালে component আবার render হয় না। এর দুটো প্রধান ব্যবহার আছে। প্রথমত, DOM element-এ সরাসরি পৌঁছানো, যেমন input-এ focus করা, scroll করা, video চালানো। দ্বিতীয়ত, এমন মান ধরে রাখা যা সময়ের সাথে বদলায় কিন্তু স্ক্রিনে দেখানো দরকার নেই, যেমন timer ID, আগের মান, বা একটা flag।

📖 **ধাপে ধাপে বুঝুন**

- **গঠন:** `const ref = useRef(0);` → `ref.current` হলো 0।
- **`useState` বনাম `useRef`**
  👉 State বদলালে UI আপডেট হয়। Ref বদলালে হয় না। UI-তে দেখানো লাগলে state, না লাগলে ref।
- **ব্যবহার ১: DOM ধরা**
  👉 `<input ref={inputRef} />` লিখলে render-এর পরে `inputRef.current` আসল DOM element।
- **ব্যবহার ২: টাইমারের ID**
  👉 `setInterval` থেকে পাওয়া ID ref-এ রাখলে পরে `clearInterval` করা যায়।
- **ব্যবহার ৩: আগের মান মনে রাখা**
  👉 effect-এ `prev.current = value` লিখে পরের render-এ আগের মান পাওয়া যায়।
- **ব্যবহার ৪: প্রথম render চেনা**
  👉 `isFirst` flag ref-এ রাখা।
- **কখন পড়বেন/লিখবেন**
  👉 event handler বা effect-এ। Render-এর সময় নয়।
- **Child-এর DOM পেতে**
  👉 React 19-এ `ref` সরাসরি prop হিসেবে পাঠানো যায়। পুরনো সংস্করণে `forwardRef` লাগত।

🧪 **কোড**

```jsx
import { useRef, useState, useEffect } from "react";

// ১) DOM ধরা: focus ও scroll
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
      <input ref={inputRef} placeholder="মন্তব্য" />
      <button onClick={add}>পাঠান</button>
    </div>
  );
}

// ২) মান ধরে রাখা: stopwatch
function Stopwatch() {
  const [sec, setSec] = useState(0);
  const idRef = useRef(null);

  const start = () => {
    if (idRef.current) return;          // আগেই চললে আর শুরু নয়
    idRef.current = setInterval(() => setSec(s => s + 1), 1000);
  };
  const stop = () => {
    clearInterval(idRef.current);
    idRef.current = null;
  };

  useEffect(() => stop, []);            // component মুছলে বন্ধ

  return (
    <>
      <p>{sec} সেকেন্ড</p>
      <button onClick={start}>শুরু</button>
      <button onClick={stop}>থামান</button>
    </>
  );
}

// ৩) আগের মান
function usePrevious(value) {
  const ref = useRef();
  useEffect(() => { ref.current = value; }, [value]);
  return ref.current;
}
```

⚠️ **সাধারণ ভুল**

- **UI-তে দেখানোর মান ref-এ রাখা।** ref বদলালে স্ক্রিন বদলায় না।
- **Render-এর সময় `ref.current` বদলানো।** অনির্দিষ্ট আচরণ হতে পারে।
- **প্রথম render-এ `ref.current` null।** `useEffect`-এর আগে DOM ref ব্যবহার করলে null আসে।
- **সবকিছুতে `document.querySelector` ব্যবহার।** React-এ `ref` ব্যবহার করুন।

🎯 **ফলো-আপ প্রশ্ন**

- **`useRef` কি state-এর বদলি?**
  👉 না। ref বদলালে re-render হয় না।
- **Ref বদলালে কেন render হয় না?**
  👉 React শুধু state ও props বদলে নজর রাখে।
- **`forwardRef` কী?**
  👉 পুরনো React-এ child component-এর ভেতরের DOM-এ parent-এর ref পাঠানোর উপায়।

📝 **এক লাইনে মনে রাখুন:** ref = এমন বাক্স, যা বদলালে স্ক্রিন বদলায় না।

🔮 **আজ ও ভবিষ্যতে:** animation, video player, ফর্ম focus, third-party লাইব্রেরি সংযোগে সবখানে লাগে।

---

## 4️⃣2️⃣ React keys কী এবং list-এ কেন গুরুত্বপূর্ণ?

> 🎤 **পূর্ণ উত্তর:** List রেন্ডার করার সময় প্রতিটা item-এ একটি `key` prop দিতে হয়। Key একটি অনন্য ও স্থির পরিচয়, যা দিয়ে React বোঝে কোন item যোগ হলো, মুছলো বা জায়গা বদলালো। সঠিক key থাকলে React শুধু বদলানো item আপডেট করে এবং বাকিদের state ঠিক রাখে। ভুল key (যেমন ক্রম বদলানো list-এ index) থাকলে React ভুল item-এ পুরনো state বসিয়ে দিতে পারে, ফলে বাগ ও অতিরিক্ত কাজ হয়। সবচেয়ে ভালো key হলো ডেটার নিজস্ব ID।

📖 **ধাপে ধাপে বুঝুন**

- **Key ছাড়া কী হয়?**
  👉 React সতর্কতা দেয়, এবং ক্রম ধরে item মেলায়, যা অনেক সময় ভুল।
- **Key কীভাবে কাজ করে?**
  👉 Diffing-এর সময় React পুরনো ও নতুন list-এ একই key-এর item মেলায়। key মিললে সেটাই "আগের সেই item"।
- **Key-র ৩টি গুণ**
  👉 অনন্য (siblings-এর মধ্যে), স্থির (render-এ বদলায় না), পূর্বানুমেয় (`Math.random()` নয়)।
- **Index কেন সমস্যা?**
  👉 তিনটি item: A(0), B(1), C(2)। A মুছলে B হয় 0, C হয় 1। React ভাবে 0 আর 1 আগের মতোই আছে, ভেতরের state (যেমন input-এ লেখা) আগের জায়গাতেই থেকে যায়। ফলে ভুল item-এ ভুল state লেগে যায়।
- **Index কখন নিরাপদ?**
  👉 list স্থির, কখনো বদলায় না, ক্রম বদলায় না, আর item-এর কোনো ID নেই।
- **Key দিয়ে component রিসেট করা**
  👉 key বদলালে React পুরনো component মুছে নতুন বানায়, এটা state রিসেট করার কাজে লাগে।
- **কোথায় key বসবে**
  👉 `map` থেকে ফেরত দেওয়া সবচেয়ে বাইরের element-এ। Fragment-এ লাগলে `<Fragment key=...>` লিখতে হয়।

🧪 **কোড**

```jsx
import { useState, Fragment } from "react";

function TodoList() {
  const [todos, setTodos] = useState([
    { id: "a1", text: "পড়া" },
    { id: "b2", text: "খেলা" },
    { id: "c3", text: "ঘুম" },
  ]);

  const remove = id => setTodos(todos.filter(t => t.id !== id));

  return (
    <ul>
      {todos.map(t => (
        // ✅ স্থির ID দিয়ে key
        <li key={t.id}>
          <input defaultValue={t.text} />
          <button onClick={() => remove(t.id)}>মুছুন</button>
        </li>
      ))}
    </ul>
  );
}

// ❌ index key: প্রথমটা মুছলে input-এর লেখা ভুল item-এ চলে যেতে পারে
// {todos.map((t, i) => <li key={i}>...</li>)}

// Fragment-এ key
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

// key বদলে component রিসেট
// <Profile key={userId} userId={userId} />
```

⚠️ **সাধারণ ভুল**

- **`key={Math.random()}`।** প্রতি render-এ নতুন key হয়, সব item মুছে নতুন করে বানাতে হয়।
- **Index ব্যবহার করে list-এ যোগ/মোছা/সাজানো।** state এলোমেলো হয়।
- **Key child component-এর ভেতরে (`<li>`-এর ভেতরের element-এ) দেওয়া।** key বসবে `map`-এর সবচেয়ে বাইরের element-এ।
- **Key-কে prop হিসেবে পড়ার চেষ্টা।** `props.key` পাওয়া যায় না।

🎯 **ফলো-আপ প্রশ্ন**

- **Key কি পুরো অ্যাপে অনন্য হতে হবে?**
  👉 না, শুধু একই parent-এর ভাইবোনদের মধ্যে।
- **ID না থাকলে কী করবেন?**
  👉 ডেটা তৈরির সময়ই `crypto.randomUUID()` দিয়ে ID বানিয়ে রাখুন, রেন্ডারের সময় নয়।
- **Key দিয়ে state রিসেট কীভাবে হয়?**
  👉 key বদলালে React মনে করে এটা সম্পূর্ণ নতুন component, তাই আগের state মুছে ফেলে।

📝 **এক লাইনে মনে রাখুন:** key = item-এর স্থির পরিচয়, index নয়, ID।

🔮 **আজ ও ভবিষ্যতে:** database-এর `id` সরাসরি key বানানো সবচেয়ে নিরাপদ অভ্যাস।

---

## 4️⃣3️⃣ State ও Props-এর পার্থক্য কী?

> 🎤 **পূর্ণ উত্তর:** Props হলো parent থেকে child-এ পাঠানো ডেটা, যা child শুধু পড়তে পারে, বদলাতে পারে না। State হলো component-এর নিজস্ব ডেটা, যা সে নিজেই setter দিয়ে বদলাতে পারে এবং বদলালে component আবার render হয়। Props-এর মালিক parent, আর state-এর মালিক সেই component নিজে। দুটোই UI-কে প্রভাবিত করে এবং বদলালে re-render ঘটায়। একই ডেটা দুই বা ততোধিক component-এর লাগলে state-কে তাদের কাছের সাধারণ parent-এ তুলে নিয়ে (lifting state up) props হিসেবে নিচে পাঠাতে হয়।

📖 **ধাপে ধাপে বুঝুন**

- **মালিকানা**
  👉 Props = parent-এর। State = component-এর নিজের।
- **পরিবর্তন**
  👉 Props শুধু parent বদলাতে পারে। State component নিজে `setState` দিয়ে।
- **একই ডেটা দুই চেহারা**
  👉 Parent-এ যেটা state, child-এ সেটাই props।
- **Re-render**
  👉 state বা props বদলালে component render হয়।
- **Lifting state up**
  👉 দুই ভাইবোন component একই ডেটা চাইলে state তাদের parent-এ নেওয়া হয়।
- **কখন state, কখন props, কখন কোনোটাই নয়**
  👉 সময়ের সাথে বদলায় ও স্ক্রিনে দেখাতে হয় → state। অন্যজন দিচ্ছে → props। অন্য state বা props থেকে হিসাব করা যায় → কোনোটাই নয়, সরাসরি হিসাব করুন।

| বৈশিষ্ট্য | Props | State |
|---|---|---|
| মালিক | parent | component নিজে |
| বদলানো যায়? | না (read-only) | হ্যাঁ (setter দিয়ে) |
| উদ্দেশ্য | ডেটা/function পাঠানো | নিজস্ব পরিবর্তনশীল ডেটা রাখা |
| বদলালে | re-render | re-render |
| উদাহরণ | `<Card title="Hi" />` | `useState(0)` |

🧪 **কোড**

```jsx
// Lifting state up: দুটো ভাইবোন একই তাপমাত্রা দেখায়
function Converter() {
  const [celsius, setCelsius] = useState(0);        // state এখানে

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
  const f = celsius * 9 / 5 + 32;                    // হিসাব করা, আলাদা state নয়
  return <p>{f} °F</p>;
}
```

⚠️ **সাধারণ ভুল**

- **Props সরাসরি বদলানো।** child-এ `props.value = 5` করা যায় না।
- **Derived ডেটা আলাদা state-এ রাখা।** `fahrenheit` আলাদা state বানালে দুটো আলাদা হয়ে যেতে পারে।
- **খুব উপরে state তুলে ফেলা।** শুধু যতটা দরকার ততটাই তুলুন, নইলে অযথা সব render হয়।

🎯 **ফলো-আপ প্রশ্ন**

- **Child কীভাবে parent-এর state বদলায়?**
  👉 Parent একটা callback function props হিসেবে দেয়, child সেটা ডাকে।
- **Props বদলালে কি child-এর state রিসেট হয়?**
  👉 না। state থেকে যায়, শুধু `key` বদলালে রিসেট হয়।
- **Props আর state দুটোই কি async?**
  👉 Props parent থেকে আসে, আর state আপডেট batch হয়। দুটোই render-এর snapshot-এ স্থির।

📝 **এক লাইনে মনে রাখুন:** Props = ধার, State = নিজের।

🔮 **আজ ও ভবিষ্যতে:** "state কোথায় থাকবে" ঠিক করাই React ডিজাইনের মূল দক্ষতা।

---

## 4️⃣4️⃣ React-এ conditional rendering কীভাবে কাজ করে?

> 🎤 **পূর্ণ উত্তর:** Conditional rendering মানে শর্ত অনুযায়ী ভিন্ন UI দেখানো। React-এ এর জন্য আলাদা কোনো সিনট্যাক্স নেই, সাধারণ JavaScript-ই কাজ করে। আমি `if/else` দিয়ে early return, JSX-এর ভেতরে ternary `condition ? A : B`, আর "দেখাও অথবা কিছু না" ধরনের ক্ষেত্রে `&&` ব্যবহার করি। Component `null`, `false` বা `undefined` ফেরত দিলে কিছুই দেখানো হয় না। `&&` ব্যবহার করার সময় বাঁদিকে `0` এলে স্ক্রিনে `0` ছাপা হয়, তাই সবসময় বুলিয়ান শর্ত (`count > 0`) লিখি।

📖 **ধাপে ধাপে বুঝুন**

- **পদ্ধতি ১: `if` + early return**
  👉 `loading`, `error`, খালি ডেটার মতো অবস্থা আগে সামলে ফেলুন, তারপর মূল UI লিখুন।
- **পদ্ধতি ২: Ternary**
  👉 দুটোর একটা: `{isLoggedIn ? <Home /> : <Login />}`।
- **পদ্ধতি ৩: `&&`**
  👉 একটা অংশ দেখাবে বা দেখাবে না: `{error && <ErrorMsg />}`।
- **পদ্ধতি ৪: ভেরিয়েবলে রেখে**
  👉 `let content; if (...) content = <A />; else content = <B />;` তারপর `{content}`।
- **পদ্ধতি ৫: object/switch দিয়ে বহু অবস্থা**
  👉 `status` অনুযায়ী ৪-৫ রকম UI হলে `switch` বা lookup object পরিষ্কার।
- **`null` ফেরত**
  👉 component নিজেই ঠিক করে সে কিছু দেখাবে না।
- **CSS দিয়ে লুকানো বনাম না-রেন্ডার করা**
  👉 `display: none` হলে component থাকে (state থাকে), কিন্তু শর্ত দিয়ে না-রেন্ডার করলে component মুছে যায় (state হারায়)।
- **তিন অবস্থার প্যাটার্ন**
  👉 loading → error → empty → data, প্রতিটি আলাদাভাবে সামলান।

🧪 **কোড**

```jsx
function Orders({ loading, error, orders, user }) {
  // early return: আগে সব বিশেষ অবস্থা
  if (loading) return <p>লোড হচ্ছে...</p>;
  if (error) return <p style={{ color: "red" }}>সমস্যা: {error}</p>;
  if (orders.length === 0) return <p>এখনো কোনো অর্ডার নেই</p>;

  return (
    <div>
      {/* ternary */}
      <h2>{user ? `স্বাগতম, ${user.name}` : "অতিথি"}</h2>

      {/* && : বুলিয়ান শর্ত দিন */}
      {user?.isAdmin && <button>অ্যাডমিন প্যানেল</button>}
      {orders.length > 0 && <p>মোট {orders.length}টি অর্ডার</p>}

      <ul>
        {orders.map(o => <li key={o.id}>{o.title}</li>)}
      </ul>
    </div>
  );
}

// বহু অবস্থা: lookup object
function StatusBadge({ status }) {
  const map = {
    pending: <span>⏳ অপেক্ষায়</span>,
    paid: <span>✅ পরিশোধিত</span>,
    cancelled: <span>❌ বাতিল</span>,
  };
  return map[status] ?? null;
}
```

⚠️ **সাধারণ ভুল**

- **`{count && <X />}`।** `count` 0 হলে স্ক্রিনে `0` দেখায়। `count > 0 && ...` লিখুন।
- **Nested ternary এ জট পাকানো।** দুইয়ের বেশি স্তর হলে early return বা আলাদা component ব্যবহার করুন।
- **Hook শর্তের ভেতরে ডাকা।** `if (x) { useState() }` ভুল। Early return-এর **আগে** সব Hook ডাকুন।
- **শর্ত দিয়ে component মুছে state হারানো।** state ধরে রাখা দরকার হলে CSS দিয়ে লুকান বা state উপরে তুলুন।

🎯 **ফলো-আপ প্রশ্ন**

- **`false`, `null`, `undefined` রেন্ডার করলে কী হয়?**
  👉 কিছুই দেখায় না। কিন্তু `0` ও `""` (শূন্য string) অন্যরকম: `0` ছাপা হয়।
- **Early return-এর আগে Hook ডাকা যাবে কি?**
  👉 না, সব Hook আগে ডাকতে হয়, নইলে Hook-এর ক্রম বদলে যায়।
- **কীভাবে একাধিক শর্ত পরিষ্কার রাখবেন?**
  👉 আলাদা ছোট component বানান বা lookup object ব্যবহার করুন।

📝 **এক লাইনে মনে রাখুন:** React-এ শর্ত মানে সাধারণ JavaScript, আর `&&`-এ `0` থেকে সাবধান।

🔮 **আজ ও ভবিষ্যতে:** প্রতিটি অ্যাপের loading, error, empty, success অবস্থায় এটা লাগে।

---

## 4️⃣5️⃣ React.memo কী এবং কখন ব্যবহার করবেন?

> 🎤 **পূর্ণ উত্তর:** `React.memo` একটি higher-order component, যা একটা component-কে মুড়ে দেয়, যাতে তার props আগের render-এর মতোই থাকলে সে আবার render না হয়। সাধারণত parent render হলে তার সব child-ও render হয়, props না বদলালেও। `memo` প্রতিটি prop আগেরটার সাথে shallow তুলনা (`Object.is`) করে, সব মিললে আগের ফলাফল পুনরায় ব্যবহার করে। কিন্তু object, array ও function প্রতি render-এ নতুন reference পায়, তাই এগুলো props হলে `useMemo` ও `useCallback` দিয়ে স্থির রাখতে হয়। `memo` শুধু তখনই ব্যবহার করা উচিত যখন component ভারী ও ঘন ঘন একই props নিয়ে render হয়, এবং আগে Profiler দিয়ে সমস্যা মেপে নেওয়া উচিত।

📖 **ধাপে ধাপে বুঝুন**

- **সমস্যা:** parent-এর state বদলাল → parent render → সব child render, এমনকি যারা কিছুই বদলায়নি।
- **`memo` কী করে?**
  👉 render-এর আগে নতুন ও পুরনো props তুলনা করে। সব সমান হলে render বাদ।
- **Shallow তুলনা মানে**
  👉 প্রতিটি prop `===` দিয়ে মেলানো। `{a:1}` আর অন্য একটা `{a:1}` সমান নয়, কারণ আলাদা reference।
- **Reference সমস্যার সমাধান**
  👉 `useCallback` function স্থির রাখে। `useMemo` object/array/মান স্থির রাখে।
- **`memo` যা আটকাতে পারে না**
  👉 component-এর নিজের state বদলানো, বা সে যে Context পড়ে তার বদলানো।
- **কাস্টম তুলনা**
  👉 `memo(Component, (prev, next) => ...)`। `true` ফেরত দিলে render বাদ। সাধারণত দরকার হয় না।
- **কখন ব্যবহার করবেন**
  👉 ভারী component, বড় list-এর row, চার্ট, যেখানে parent ঘন ঘন render হয় কিন্তু props কম বদলায়।
- **কখন করবেন না**
  👉 ছোট ও হালকা component-এ। তুলনারও খরচ আছে, কোডও জটিল হয়।
- **React Compiler**
  👉 নতুন কম্পাইলার অনেক ক্ষেত্রে স্বয়ংক্রিয়ভাবে memoization করে দেয়, তাই হাতে `memo` দেওয়ার দরকার কমছে।

🧪 **কোড**

```jsx
import { memo, useState, useCallback, useMemo } from "react";

// ভারী child: memo দিয়ে মোড়ানো
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
    { id: 1, name: "ক্যামেরা" },
    { id: 2, name: "লেন্স" },
  ]);
  const [dark, setDark] = useState(false);   // অসম্পর্কিত state

  // ❌ useCallback ছাড়া: প্রতি render-এ নতুন function, তাই memo কাজ করত না
  // const remove = id => setItems(items.filter(i => i.id !== id));

  // ✅ স্থির function (আগের মান নিতে functional update)
  const remove = useCallback(
    id => setItems(prev => prev.filter(i => i.id !== id)),
    []
  );

  // ✅ ভারী হিসাব স্থির রাখা
  const total = useMemo(() => items.length * 100, [items]);

  return (
    <div className={dark ? "dark" : ""}>
      <button onClick={() => setDark(d => !d)}>থিম বদলান</button>
      <p>মোট: {total}</p>
      <ul>
        {items.map(i => <Row key={i.id} item={i} onRemove={remove} />)}
      </ul>
    </div>
  );
}
// থিম বদলালে Row আর render হয় না (console-এ নতুন লেখা আসে না)।
```

⚠️ **সাধারণ ভুল**

- **সবখানে `memo` দেওয়া।** তুলনার খরচ আছে, অনেক সময় লাভের চেয়ে লোকসান।
- **`memo` দিয়ে inline function/object পাঠানো।** `onClick={() => ...}` বা `style={{...}}` প্রতিবার নতুন, তাই `memo` অকেজো।
- **মাপার আগেই optimize করা।** React DevTools Profiler দিয়ে আগে দেখুন কোথায় ধীর।
- **`memo` ভেবে নেওয়া যে Context-এর render-ও আটকাবে।** আটকাবে না।

🎯 **ফলো-আপ প্রশ্ন**

- **`memo`, `useMemo` ও `useCallback`-এর পার্থক্য?**
  👉 `memo` component-কে মোড়ায়। `useMemo` একটি হিসাব করা মান মনে রাখে। `useCallback` একটি function-এর reference মনে রাখে।
- **Props-এ object পাঠালে `memo` কেন কাজ করে না?**
  👉 প্রতি render-এ নতুন reference তৈরি হয়, তাই shallow তুলনায় আলাদা ধরা পড়ে।
- **`memo` কি সবসময় render আটকায়?**
  👉 না, নিজের state/context বদলালে বা props সত্যিই বদলালে render হয়।

📝 **এক লাইনে মনে রাখুন:** props না বদলালে render বাদ, কিন্তু reference স্থির রাখতে ভুলবেন না।

🔮 **আজ ও ভবিষ্যতে:** React Compiler ভবিষ্যতে হাতে হাতে memoization অনেক কমিয়ে দেবে, তবু ধারণাটা ইন্টারভিউয়ে আসে।
