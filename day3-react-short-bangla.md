# 🔵 React Fundamentals — স্টাডি গাইড ও সংক্ষিপ্ত উত্তর (বাংলা)

**Day 3 টপিক:** Components, Hooks & State Management

## 📘 কীভাবে পড়লে সবচেয়ে ভালো বুঝবেন

1. **🎤 বলুন** অংশটা আগে পড়ুন, এটাই ইন্টারভিউয়ে বলার উত্তর।
2. **📌 বুঝে নিন** অংশে প্রতিটা পয়েন্টের নিচে `👉` চিহ্নের লাইনটা পড়ুন, ওটাই আসল ব্যাখ্যা।
3. **🧪 কোড** নিজে একটা React প্রজেক্টে (Vite বা Next.js) লিখে চালিয়ে ফল মিলিয়ে দেখুন।
4. শেষে বই বন্ধ করে নিজের ভাষায় উত্তরটা মুখে বলে দেখুন।

---

## 3️⃣1️⃣ React কী এবং এটা কোন সমস্যার সমাধান করে?

> 🎤 **বলুন:** React হলো Meta-র তৈরি একটা JavaScript library, যা দিয়ে user interface বানানো হয়। UI-কে ছোট ছোট পুনঃব্যবহারযোগ্য component-এ ভাগ করা হয়। আগে ডেটা বদলালে হাতে হাতে DOM বদলাতে হতো, ফলে কোড জটিল হতো আর UI ও ডেটা মিলতো না। React-এ আমি শুধু বলি UI কেমন দেখাবে, আর ডেটা বদলালে React নিজেই স্ক্রিন আপডেট করে।

📌 **বুঝে নিন**

- **React একটা library, পুরো framework নয়**
  👉 এটা শুধু UI সামলায়। routing, ডেটা আনা ইত্যাদির জন্য আলাদা টুল (Next.js, React Router) লাগে।
- **Component-based**
  👉 লেগো ব্লকের মতো। একটা Button একবার বানালে সব জায়গায় ব্যবহার করা যায়।
- **Declarative**
  👉 "কীভাবে বদলাতে হবে" লিখি না, শুধু লিখি "ডেটা এমন হলে UI এমন দেখাবে"। বাকি কাজ React করে।
- **Virtual DOM দিয়ে দ্রুত আপডেট**
  👉 পুরো পাতা না এঁকে React শুধু যেটুকু বদলেছে সেটুকু আপডেট করে।
- **One-way data flow**
  👉 ডেটা উপর থেকে নিচে (parent থেকে child-এ) যায়, তাই কোথা থেকে কী বদলালো খুঁজে পাওয়া সহজ।

🧪 **কোড**

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// ব্যবহার: একই component বারবার
<Welcome name="Alamin" />
<Welcome name="Rahim" />
```

🔮 **আজ ও ভবিষ্যতে:** Next.js, React Native সবকিছুর ভিত্তি React। এটা শেখা মানে প্রায় সব আধুনিক frontend চাকরির দরজা খোলা।

---

## 3️⃣2️⃣ JSX কী এবং React-এ কেন ব্যবহার হয়?

> 🎤 **বলুন:** JSX হলো JavaScript-এর ভেতরে HTML-এর মতো করে UI লেখার সিনট্যাক্স। ব্রাউজার এটা সরাসরি বোঝে না, Babel বা কম্পাইলার এটাকে সাধারণ JavaScript function call-এ বদলে দেয়। এতে UI-এর গঠন আর তার লজিক এক জায়গায় থাকে, ফলে কোড পড়া সহজ হয়।

📌 **বুঝে নিন**

- **JSX ≠ HTML**
  👉 দেখতে HTML-এর মতো, কিন্তু আসলে JavaScript। শেষে এটা `React.createElement` ধরনের call হয়ে যায়।
- **একটাই root element লাগে**
  👉 একাধিক element ফেরত দিতে চাইলে `<div>` বা খালি `<>...</>` (Fragment) দিয়ে মুড়ে দিতে হয়।
- **`class`-এর বদলে `className`**
  👉 `class` JavaScript-এর শব্দ, তাই JSX-এ `className`। একইভাবে `for` হয় `htmlFor`।
- **সব tag বন্ধ করতে হয়**
  👉 `<img />`, `<input />` এভাবে শেষে `/` দিতে হবে।
- **`{ }` দিয়ে JavaScript বসানো**
  👉 `{name}`, `{2 + 3}`, `{list.map(...)}` চলে। কিন্তু `if` বা `for` সরাসরি চলে না, শুধু expression চলে।

🧪 **কোড**

```jsx
const name = "Alamin";
const el = (
  <div className="card">
    <h2>Hello, {name}</h2>
    <p>2 + 3 = {2 + 3}</p>
    <img src="a.png" alt="photo" />
  </div>
);

// ভেতরে JSX আসলে এটা:
// React.createElement("div", { className: "card" }, ...)
```

🔮 **আজ ও ভবিষ্যতে:** Next.js, Vite সব JSX সাপোর্ট করে। TypeScript-এর সাথে এটা TSX হয়ে যায়।

---

## 3️⃣3️⃣ Functional ও Class component-এর পার্থক্য কী?

> 🎤 **বলুন:** Functional component হলো একটা সাধারণ function যা JSX ফেরত দেয়, আর state ও lifecycle-এর কাজ Hooks দিয়ে করে। Class component `React.Component` থেকে extend করে, `render()` method থাকে এবং `this.state` ও lifecycle method ব্যবহার করে। এখন সবাই functional লেখে কারণ এটা ছোট, সহজ, আর `this` নিয়ে ঝামেলা নেই।

📌 **বুঝে নিন**

- **Functional → function + Hooks**
  👉 `useState`, `useEffect` দিয়ে state ও side effect সামলায়।
- **Class → `render()` + `this.state`**
  👉 `this.setState()` দিয়ে state বদলায়, আর `componentDidMount` ইত্যাদি method আছে।
- **Class-এ `this` নিয়ে ঝামেলা**
  👉 method-এ `this` হারিয়ে যায়, তাই `bind` বা arrow function লাগে। Functional-এ এই সমস্যাই নেই।
- **একটি ব্যতিক্রম: Error Boundary**
  👉 error ধরার component এখনও class দিয়েই বানাতে হয়।

| বৈশিষ্ট্য | Functional | Class |
|---|---|---|
| লেখা | function | `class ... extends React.Component` |
| State | `useState` | `this.state` |
| Lifecycle | `useEffect` | `componentDidMount` ইত্যাদি |
| `this` | লাগে না | লাগে |
| বর্তমান পছন্দ | ✅ হ্যাঁ | পুরনো কোডে |

🧪 **কোড**

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

🔮 **আজ ও ভবিষ্যতে:** নতুন সব প্রজেক্ট functional। Class শুধু পুরনো কোড পড়তে বুঝতে হয়।

---

## 3️⃣4️⃣ Virtual DOM কী এবং React এটা কীভাবে ব্যবহার করে?

> 🎤 **বলুন:** Virtual DOM হলো আসল DOM-এর একটা হালকা JavaScript object কপি। State বদলালে React নতুন একটা Virtual DOM বানায়, আগেরটার সাথে তুলনা করে (diffing), আর ঠিক যে অংশ বদলেছে শুধু সেটুকু আসল DOM-এ একসাথে আপডেট করে। এই পুরো প্রক্রিয়ার নাম reconciliation।

📌 **বুঝে নিন**

- **আসল DOM-এ বারবার হাত দেওয়া ধীর**
  👉 প্রতিবার সরাসরি বদলালে ব্রাউজারকে layout ও paint নতুন করে করতে হয়।
- **ধাপ ১: নতুন Virtual DOM তৈরি**
  👉 state বা props বদলালে React মেমরিতে নতুন UI-র ছবি আঁকে।
- **ধাপ ২: পুরনোটার সাথে তুলনা (diffing)**
  👉 দুই ছবি মিলিয়ে দেখে ঠিক কোথায় তফাত।
- **ধাপ ৩: শুধু তফাতটুকু আসল DOM-এ**
  👉 পুরো পাতা নয়, শুধু বদলানো টুকরোটা। যেমন শুধু একটা লেখা বদলালে শুধু সেটাই বদলায়।
- **List-এ `key` diffing-কে সাহায্য করে**
  👉 key দিয়ে React বোঝে কোন item কোনটা।

🧪 **কোড**

```jsx
function App() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Static title</h1>            {/* এটা বদলায় না, DOM-এ ছোঁয়া হয় না */}
      <p>Count: {count}</p>            {/* শুধু এই লেখাটা আপডেট হয় */}
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** React-এর রেন্ডারিং কীভাবে কাজ করে তা বোঝা performance সমস্যা ধরতে অপরিহার্য।

---

## 3️⃣5️⃣ useState hook উদাহরণসহ ব্যাখ্যা করুন।

> 🎤 **বলুন:** `useState` হলো functional component-এ state রাখার hook। এটা একটা array ফেরত দেয়: বর্তমান মান আর সেটা বদলানোর function। Setter ডাকলে মান বদলায় এবং component আবার render হয়। State সরাসরি বদলানো যায় না, সবসময় setter দিয়ে বদলাতে হয়।

📌 **বুঝে নিন**

- **সিনট্যাক্স: `const [value, setValue] = useState(initial)`**
  👉 `initial` হলো শুরুর মান। array destructuring দিয়ে দুটো জিনিস পাই।
- **Setter ডাকলে re-render হয়**
  👉 React নতুন মান নিয়ে component-টা আবার চালায় এবং UI আপডেট করে।
- **সরাসরি বদলানো যাবে না**
  👉 `count++` বা `arr.push()` করলে React বুঝতেই পারে না। সবসময় `setCount(...)`।
- **আগের মানের উপর নির্ভর করলে function দিন**
  👉 `setCount(prev => prev + 1)`। এতে একাধিক আপডেট একসাথে এলেও ঠিক থাকে।
- **Object/array-তে নতুন কপি বানান**
  👉 `setUser({ ...user, age: 21 })`। পুরনোটা বদলালে React পরিবর্তন ধরে না।
- **Setter ডাকার পরপরই state পুরনো থাকে**
  👉 নতুন মান পাওয়া যায় পরের render-এ, ঠিক সেই লাইনে নয়।

🧪 **কোড**

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
        বয়স বাড়াও ({user.age})
      </button>
    </div>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** form, modal, toggle, সব UI-র ভিত্তি `useState`।

---

## 3️⃣6️⃣ useEffect hook কী এবং এর ব্যবহার কী কী?

> 🎤 **বলুন:** `useEffect` দিয়ে component render হওয়ার পরে side effect চালানো যায়, যেমন API থেকে ডেটা আনা, timer, event listener বা DOM বদলানো। দ্বিতীয় argument হলো dependency array, যা ঠিক করে effect কখন চলবে। Effect থেকে একটা cleanup function ফেরত দিলে component মুছে গেলে বা effect আবার চলার আগে সেটা চলে।

📌 **বুঝে নিন**

- **Dependency array না দিলে → প্রতি render-এ চলে**
  👉 সাধারণত এটা চাওয়া হয় না, অনেক সময় অসীম লুপ হয়।
- **`[]` (খালি) → শুধু প্রথমবার চলে**
  👉 পাতা প্রথম খোলার সময় একবার ডেটা আনতে এটা ব্যবহার করা হয়।
- **`[a, b]` → a বা b বদলালে চলে**
  👉 ID বদলালে নতুন ডেটা আনার মতো কাজে।
- **Cleanup function**
  👉 `return () => ...`। timer বন্ধ করা বা listener সরানো, নইলে memory leak হয়।
- **Dev mode-এ Strict Mode effect দুবার চালায়**
  👉 এটা ইচ্ছাকৃত, cleanup ঠিক আছে কি না যাচাই করতে। Production-এ একবার।
- **যে মান render-এর সময়েই বের করা যায় তার জন্য effect লাগে না**
  👉 শুধু বাইরের জগতের সাথে কাজের জন্য effect।

🧪 **কোড**

```jsx
import { useState, useEffect } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  // ১) শুধু প্রথমবার ডেটা আনা
  useEffect(() => {
    fetch("/api/users")
      .then(res => res.json())
      .then(setUsers);
  }, []);

  // ২) timer + cleanup
  useEffect(() => {
    const id = setInterval(() => console.log("tick"), 1000);
    return () => clearInterval(id);   // মুছে গেলে timer বন্ধ
  }, []);

  return <p>মোট: {users.length}</p>;
}
```

🔮 **আজ ও ভবিষ্যতে:** Next.js-এ ডেটা আনার জন্য এখন server component বা TanStack Query বেশি ব্যবহার হয়, তবু useEffect বোঝা জরুরি।

---

## 3️⃣7️⃣ Controlled ও Uncontrolled component-এর পার্থক্য কী?

> 🎤 **বলুন:** Controlled component-এ form input-এর মান React state-এ থাকে, `value` আর `onChange` দিয়ে নিয়ন্ত্রণ হয়, তাই React-ই একমাত্র সত্যের উৎস। Uncontrolled component-এ মান থাকে ব্রাউজারের DOM-এ, আর দরকারের সময় `ref` দিয়ে পড়া হয়। Validation বা তাৎক্ষণিক প্রতিক্রিয়ার জন্য controlled ভালো, আর সহজ বা file input-এর জন্য uncontrolled।

📌 **বুঝে নিন**

- **Controlled → `value` + `onChange`**
  👉 প্রতিটা অক্ষর টাইপ করলে state বদলায়, আর input সেই state-ই দেখায়।
- **Uncontrolled → `ref` দিয়ে পড়া**
  👉 টাইপ করার সময় React কিছু জানে না। জমা দেওয়ার সময় `ref.current.value` পড়ি।
- **Controlled-এর সুবিধা**
  👉 লাইভ validation, বোতাম বন্ধ/চালু, মান ফরম্যাট করা সহজ।
- **File input সবসময় uncontrolled**
  👉 `<input type="file" />`-এর মান কোড দিয়ে সেট করা যায় না।
- **`value` দিয়ে `onChange` না দিলে input আটকে যায়**
  👉 React মান ধরে রাখে কিন্তু বদলানোর উপায় নেই, তাই টাইপ হয় না।

🧪 **কোড**

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
      <button onClick={() => alert(ref.current.value)}>দেখাও</button>
    </>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** বড় form-এ React Hook Form uncontrolled ধরনে কাজ করে performance ভালো রাখতে।

---

## 3️⃣8️⃣ React-এ props কী এবং কীভাবে পাঠানো হয়?

> 🎤 **বলুন:** Props হলো parent component থেকে child component-কে পাঠানো ডেটা, HTML attribute-এর মতো করে লেখা হয়। Props শুধু পড়া যায়, child সেটা বদলাতে পারে না। ডেটার সাথে function-ও পাঠানো যায়, যাতে child parent-কে জানাতে পারে। `children` নামের বিশেষ prop দিয়ে ট্যাগের ভেতরের কনটেন্ট পাঠানো যায়।

📌 **বুঝে নিন**

- **পাঠানো: `<Card title="Hi" />`**
  👉 attribute-এর মতো লিখলেই child-এর কাছে props object হয়ে পৌঁছায়।
- **নেওয়া: destructuring**
  👉 `function Card({ title })`। `props.title` লেখার চেয়ে পরিষ্কার।
- **Props read-only**
  👉 child নিজে `props.title = ...` করতে পারে না। বদলাতে হলে parent-এর state বদলাতে হয়।
- **Function পাঠানো যায়**
  👉 `<Button onClick={handleClick} />`। child থেকে parent-কে খবর দেওয়ার উপায়।
- **`children` prop**
  👉 `<Box>ভেতরের লেখা</Box>` লিখলে "ভেতরের লেখা" `children` হয়ে পৌঁছায়।
- **Default মান**
  👉 `function Card({ title = "Untitled" })`

🧪 **কোড**

```jsx
function Card({ title, price = 0, onBuy, children }) {
  return (
    <div>
      <h3>{title} — {price} টাকা</h3>
      {children}
      <button onClick={onBuy}>কিনুন</button>
    </div>
  );
}

function App() {
  return (
    <Card title="ক্যামেরা" price={500} onBuy={() => alert("কেনা হলো")}>
      <p>৩ দিনের ভাড়া</p>
    </Card>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** TypeScript-এ props-এর type লিখে ভুল আগেই ধরা যায়।

---

## 3️⃣9️⃣ Prop drilling কী এবং কীভাবে এড়ানো যায়?

> 🎤 **বলুন:** Prop drilling হলো একটা ডেটা অনেক স্তর নিচের component-এ পৌঁছানোর জন্য মাঝের সব component দিয়ে props পার করানো, যদিও মাঝের component-গুলোর ওই ডেটার দরকার নেই। এতে কোড জটিল ও বদলানো কঠিন হয়। এড়ানোর উপায়: Context API, component composition (`children`), বা Redux, Zustand-এর মতো state management library।

📌 **বুঝে নিন**

- **সমস্যা: মাঝের component শুধু ডাকপিয়ন**
  👉 `App → Layout → Sidebar → Avatar`। শুধু Avatar-এর `user` দরকার, কিন্তু সবাইকে ধরে ধরে পাঠাতে হয়।
- **সমাধান ১: Context API**
  👉 উপরে একবার ডেটা রাখো, যে কোনো নিচের component সরাসরি নিয়ে নেবে।
- **সমাধান ২: Composition**
  👉 তৈরি করা component-কে `children` হিসেবে পাঠালে মাঝের স্তর কমে যায়।
- **সমাধান ৩: Zustand/Redux**
  👉 পুরো অ্যাপের ডেটা এক আলাদা store-এ, যেখান থেকে যে কেউ নিতে পারে।
- **সব সময় এড়ানো দরকার নেই**
  👉 ১-২ স্তর হলে props পাঠানোই সহজ ও পরিষ্কার।

🧪 **কোড**

```jsx
// ❌ Prop drilling
<Layout user={user} />
function Layout({ user }) { return <Sidebar user={user} />; }
function Sidebar({ user }) { return <Avatar user={user} />; }

// ✅ Composition দিয়ে
<Layout sidebar={<Avatar user={user} />} />
function Layout({ sidebar }) { return <aside>{sidebar}</aside>; }
```

🔮 **আজ ও ভবিষ্যতে:** auth, theme, ভাষার মতো গ্লোবাল ডেটার জন্য Context বা Zustand ব্যবহার হয়।

---

## 4️⃣0️⃣ useContext hook উদাহরণসহ ব্যাখ্যা করুন।

> 🎤 **বলুন:** `useContext` দিয়ে প্রতিটা স্তরে props না পাঠিয়ে যে কোনো গভীর component সরাসরি ভাগ করা ডেটা পড়তে পারে। প্রথমে `createContext` দিয়ে context বানাই, উপরে Provider-এ `value` দিই, আর নিচে `useContext` দিয়ে সেটা নিই। Theme, logged-in user, ভাষার মতো কম বদলানো গ্লোবাল ডেটার জন্য এটা ভালো।

📌 **বুঝে নিন**

- **ধাপ ১: `createContext()`**
  👉 একটা ডেটার "চ্যানেল" তৈরি করা।
- **ধাপ ২: `Provider` দিয়ে মোড়ানো**
  👉 যে অংশে ডেটা লাগবে তাকে `<Ctx.Provider value={...}>` দিয়ে ঘিরে ফেলা।
- **ধাপ ৩: `useContext(Ctx)`**
  👉 ভেতরের যে কোনো component সরাসরি মান পেয়ে যায়।
- **Value বদলালে সব consumer আবার render হয়**
  👉 তাই খুব ঘন ঘন বদলানো ডেটা (যেমন মাউসের অবস্থান) Context-এ রাখা ঠিক নয়।
- **Provider-এর বাইরে ডিফল্ট মান পাওয়া যায়**
  👉 `createContext(defaultValue)`-এর মান।

🧪 **কোড**

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

function Page() { return <Button />; }   // কিছু পাঠাতে হয়নি

function Button() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>
      এখন: {theme}
    </button>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** Next.js অ্যাপে theme, auth, cart-এর জন্য Context খুব সাধারণ প্যাটার্ন।

---

## 4️⃣1️⃣ useRef hook কী এবং কখন ব্যবহার করবেন?

> 🎤 **বলুন:** `useRef` একটা `{ current: ... }` object ফেরত দেয়, যেটা re-render-এর মধ্যেও একই থাকে এবং এর মান বদলালে component আবার render হয় না। দুটো প্রধান ব্যবহার: DOM element-এ সরাসরি পৌঁছানো (যেমন input-এ focus করা), আর এমন মান রাখা যা বদলালে UI আপডেট দরকার নেই, যেমন timer ID।

📌 **বুঝে নিন**

- **`ref.current` বদলালে re-render হয় না**
  👉 এটাই `useState` থেকে বড় তফাত। state বদলালে UI আপডেট হয়, ref বদলালে হয় না।
- **DOM element ধরা: `<input ref={myRef} />`**
  👉 `myRef.current` তখন আসল input element। `.focus()`, `.scrollIntoView()` ডাকা যায়।
- **গোপন মান রাখা**
  👉 `setInterval`-এর id, আগের মান, ইত্যাদি, যা পরে লাগবে কিন্তু স্ক্রিনে দেখানো লাগবে না।
- **Render-এর সময় `ref.current` পড়া বা লেখা এড়ান**
  👉 এটা event handler বা effect-এর ভেতরে করুন, নইলে আচরণ অনির্দিষ্ট হতে পারে।

🧪 **কোড**

```jsx
import { useRef, useState, useEffect } from "react";

function Search() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();   // পাতা খুলতেই input-এ কার্সর
  }, []);

  return <input ref={inputRef} placeholder="খুঁজুন..." />;
}

function Timer() {
  const idRef = useRef(null);
  const [n, setN] = useState(0);

  const start = () => { idRef.current = setInterval(() => setN(x => x + 1), 1000); };
  const stop  = () => clearInterval(idRef.current);

  return (
    <>
      <p>{n}</p>
      <button onClick={start}>শুরু</button>
      <button onClick={stop}>থামাও</button>
    </>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** Form focus, scroll, video play/pause, animation লাইব্রেরি, সবখানে `useRef`।

---

## 4️⃣2️⃣ React keys কী এবং list-এ কেন গুরুত্বপূর্ণ?

> 🎤 **বলুন:** List রেন্ডার করার সময় প্রতিটা item-এ একটা অনন্য ও স্থির `key` দিতে হয়, যাতে React বুঝতে পারে কোন item যোগ হলো, মুছলো বা জায়গা বদলালো। Key না থাকলে বা ভুল key হলে React ভুল item আপডেট করতে পারে, ফলে বাগ ও ধীর গতি হয়। Key হিসেবে ডেটার ID ব্যবহার করা উচিত, list-এর ক্রম বদলাতে পারলে index নয়।

📌 **বুঝে নিন**

- **Key হলো item-এর পরিচয়পত্র**
  👉 পরিচয়পত্র দেখে React বলে দিতে পারে "এই লোকটা আগের সেই লোকই, শুধু জায়গা বদলেছে"।
- **অনন্য হতে হবে শুধু ভাইবোনদের (siblings) মধ্যে**
  👉 পুরো অ্যাপে নয়, একই list-এর মধ্যে।
- **স্থির হতে হবে**
  👉 `Math.random()` দেওয়া ভুল, কারণ প্রতি render-এ নতুন key হলে সব item নতুন করে বানাতে হয়।
- **Index key-র সমস্যা**
  👉 মাঝখান থেকে item মুছলে বা ক্রম বদলালে input-এ লেখা মান ভুল item-এ চলে যেতে পারে।
- **Index কখন চলে?**
  👉 list কখনো বদলায় না, ক্রম ঠিক থাকে, আর item-এ ID নেই, এমন ক্ষেত্রে।
- **`key` prop হিসেবে child-এ পৌঁছায় না**
  👉 এটা শুধু React-এর নিজের কাজের জন্য।

🧪 **কোড**

```jsx
const todos = [
  { id: 1, text: "পড়া" },
  { id: 2, text: "খেলা" },
];

// ✅ ঠিক
<ul>
  {todos.map(t => <li key={t.id}>{t.text}</li>)}
</ul>

// ❌ ঝুঁকিপূর্ণ (ক্রম বদলালে সমস্যা)
{todos.map((t, i) => <li key={i}>{t.text}</li>)}
```

🔮 **আজ ও ভবিষ্যতে:** ডেটাবেসের `id` সরাসরি key বানানো সবচেয়ে সহজ ও নিরাপদ অভ্যাস।

---

## 4️⃣3️⃣ State ও Props-এর পার্থক্য কী?

> 🎤 **বলুন:** Props আসে বাইরে থেকে, parent-এর কাছ থেকে, এবং child তা শুধু পড়তে পারে। State থাকে component-এর নিজের ভেতরে, এবং component নিজেই setter দিয়ে সেটা বদলাতে পারে। দুটোর যেকোনোটা বদলালে component আবার render হয়। দুই component-এর ডেটা শেয়ার করতে হলে state কাছের সাধারণ parent-এ তুলে আনা হয়।

📌 **বুঝে নিন**

- **Props → ধার করা**
  👉 অন্যের কাছ থেকে পাওয়া, শুধু ব্যবহার করা যায়, বদলানো যায় না।
- **State → নিজের**
  👉 component-এর নিজস্ব স্মৃতি, যা সে নিজে বদলাতে পারে।
- **একজনের state অন্যজনের props**
  👉 parent-এর state যখন child-কে props হিসেবে দেওয়া হয়, তখন child-এর কাছে সেটা props।
- **Lifting state up**
  👉 দুই ভাইবোনের একই ডেটা লাগলে state তাদের বাবার কাছে নিয়ে গিয়ে দুজনকে props দিয়ে পাঠানো হয়।

| বৈশিষ্ট্য | Props | State |
|---|---|---|
| কোথা থেকে আসে | parent থেকে | component-এর নিজের ভেতর |
| বদলানো যায়? | না (read-only) | হ্যাঁ (setter দিয়ে) |
| কে বদলায় | parent | component নিজে |
| বদলালে | re-render | re-render |

🧪 **কোড**

```jsx
function Parent() {
  const [count, setCount] = useState(0);        // state (Parent-এর নিজের)
  return <Child count={count} onAdd={() => setCount(count + 1)} />;
}

function Child({ count, onAdd }) {               // props (ধার করা)
  return <button onClick={onAdd}>{count}</button>;
}
```

🔮 **আজ ও ভবিষ্যতে:** "কার state কোথায় থাকবে" ঠিক করা React ডিজাইনের সবচেয়ে গুরুত্বপূর্ণ দক্ষতা।

---

## 4️⃣4️⃣ React-এ conditional rendering কীভাবে কাজ করে?

> 🎤 **বলুন:** Conditional rendering মানে শর্ত অনুযায়ী আলাদা UI দেখানো। React-এ আলাদা কোনো সিনট্যাক্স নেই, সাধারণ JavaScript-ই ব্যবহার হয়: `if/else`, ternary `? :`, আর `&&`। `null` ফেরত দিলে কিছুই দেখানো হয় না।

📌 **বুঝে নিন**

- **`if` দিয়ে early return**
  👉 শুরুতেই `if (loading) return <Spinner />;` লিখে পরে স্বাভাবিক UI।
- **Ternary: `condition ? A : B`**
  👉 দুটোর একটা দেখাতে হলে। JSX-এর ভেতরে লেখা যায়।
- **`&&`: শর্ত সত্য হলে দেখাও, নইলে কিছু না**
  👉 `{isAdmin && <AdminPanel />}`
- **`&&`-এর ফাঁদ: `0`**
  👉 `{count && <X />}` যদি `count` 0 হয় তাহলে স্ক্রিনে `0` দেখাবে। লিখুন `{count > 0 && <X />}`।
- **`null` ফেরত → কিছু দেখায় না**
  👉 component ইচ্ছে করে লুকাতে চাইলে।

🧪 **কোড**

```jsx
function Dashboard({ loading, user, items }) {
  if (loading) return <p>লোড হচ্ছে...</p>;      // early return

  return (
    <div>
      {user ? <h2>স্বাগতম, {user.name}</h2> : <a href="/login">লগইন করুন</a>}
      {user?.isAdmin && <button>অ্যাডমিন প্যানেল</button>}
      {items.length > 0 && <p>মোট {items.length}টি</p>}   {/* length && নয়! */}
    </div>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** loading, error, খালি অবস্থা (empty state), সব UI-তেই এই ৩টি প্যাটার্ন লাগে।

---

## 4️⃣5️⃣ React.memo কী এবং কখন ব্যবহার করবেন?

> 🎤 **বলুন:** `React.memo` একটা component-কে মুড়ে দেয়, যাতে তার props আগের মতোই থাকলে সে আবার render না হয়। সাধারণত parent render হলে সব child-ও render হয়, `memo` সেটা আটকায়। Props shallow তুলনা করা হয়, তাই object, array বা function props-এর জন্য `useMemo` ও `useCallback` লাগে। শুধু ভারী ও ঘন ঘন render হওয়া component-এ ব্যবহার করা উচিত।

📌 **বুঝে নিন**

- **Parent render হলে child-ও render হয়**
  👉 props না বদলালেও। এটাই অপ্রয়োজনীয় কাজ।
- **`memo` shallow তুলনা করে**
  👉 প্রতিটা prop আগের সাথে `===` দিয়ে মেলায়। সব মিললে render বাদ।
- **Object/array/function প্রতি render-এ নতুন**
  👉 `{}` বা `() => {}` লিখলে প্রতিবার নতুন reference হয়, তাই `memo` কাজ করে না। সমাধান: `useMemo` ও `useCallback`।
- **নিজের state বা context বদলালে `memo` আটকাতে পারে না**
  👉 `memo` শুধু parent-এর কারণে হওয়া re-render আটকায়।
- **সবখানে দেবেন না**
  👉 তুলনারও খরচ আছে। আগে মাপুন (React DevTools Profiler), তারপর দিন।

🧪 **কোড**

```jsx
import { memo, useState, useCallback } from "react";

const Row = memo(function Row({ name, onDelete }) {
  console.log("render:", name);
  return <li>{name} <button onClick={onDelete}>X</button></li>;
});

function List() {
  const [count, setCount] = useState(0);

  // useCallback ছাড়া প্রতিবার নতুন function, তাই memo কাজ করত না
  const handleDelete = useCallback(() => console.log("deleted"), []);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      <ul><Row name="Alamin" onDelete={handleDelete} /></ul>
    </>
  );
}
```

🔮 **আজ ও ভবিষ্যতে:** নতুন React Compiler অনেক ক্ষেত্রে এই memoization নিজেই করে দেয়, তবু ধারণাটা ইন্টারভিউয়ে আসে।
