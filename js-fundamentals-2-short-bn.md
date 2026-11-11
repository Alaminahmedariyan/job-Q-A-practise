# 🟣 JavaScript Fundamentals II — ইন্টারভিউ সংক্ষিপ্ত উত্তর (বাংলা)

**টপিক:** Arrays, Objects, ES6+ & Async

> প্রতিটি প্রশ্নে তিনটি অংশ: 🎤 **মুখে যেভাবে বলবেন**, 📌 **মূল পয়েন্ট**, 🔮 **আজকের দিনে ও ভবিষ্যতে**।

---

## 1️⃣6️⃣ Destructuring কী? Array ও object-এর উদাহরণসহ বলুন।

> 🎤 **বলুন:** জি, Destructuring হলো array বা object-এর মান সরাসরি আলাদা আলাদা variable-এ বের করে আনার সংক্ষিপ্ত উপায়। Array-তে ক্রম অনুযায়ী বের হয়, আর object-এ property-র নাম ধরে। এতে default মান, নাম বদলানো আর nested ডেটা বের করাও যায়। এতে কোড ছোট ও পরিষ্কার হয়।

📌 **মূল পয়েন্ট**
- Array → position ধরে, Object → নাম ধরে
- Default মান: `{ role = "user" }`
- নাম বদল: `{ name: userName }`
- Function parameter-এও ব্যবহার করা যায়

```javascript
let [a, b] = [1, 2];
const { name, age = 20, city: town } = { name: "Alamin", city: "Sherpur" };
[a, b] = [b, a];              // swap
```

🔮 **আজ ও ভবিষ্যতে:** React-এ `const [state, setState] = useState()` এবং props destructuring প্রতিদিনের কোড।

---

## 1️⃣7️⃣ Spread ও Rest অপারেটর কী?

> 🎤 **বলুন:** দুটোরই চিহ্ন `...`, কিন্তু কাজ উল্টো। Spread একটা array বা object-কে ছড়িয়ে দেয়, আর Rest অনেকগুলো মানকে একটা array বা object-এ জড়ো করে। Spread দিয়ে copy ও merge করি, আর Rest দিয়ে function-এ অজানা সংখ্যক argument ধরি। মনে রাখার বিষয়, Spread-এর copy shallow।

📌 **মূল পয়েন্ট**
- Spread: ছড়ানো (copy, merge, argument পাঠানো)
- Rest: জড়ো করা (সবসময় শেষ parameter)
- Copy shallow, nested object একই reference থাকে

```javascript
const merged = [...[1, 2], ...[3, 4]];
const user2 = { ...user, role: "admin" };
const sum = (...nums) => nums.reduce((a, b) => a + b, 0);
```

🔮 **আজ ও ভবিষ্যতে:** React state immutable ভাবে আপডেট করতে spread সবচেয়ে বেশি ব্যবহৃত প্যাটার্ন।

---

## 1️⃣8️⃣ map(), filter() ও reduce()-এর পার্থক্য কী?

> 🎤 **বলুন:** তিনটাই array method, মূল array না বদলে নতুন ফলাফল দেয়। `map` প্রতিটি element রূপান্তর করে একই দৈর্ঘ্যের নতুন array দেয়। `filter` শর্ত মেলা element দিয়ে ছোট array দেয়। আর `reduce` পুরো array থেকে একটিমাত্র মান বের করে, যেমন যোগফল।

📌 **মূল পয়েন্ট**
- `map` → রূপান্তর (দৈর্ঘ্য একই)
- `filter` → বাছাই (দৈর্ঘ্য কম বা সমান)
- `reduce` → একটি মানে সংক্ষেপ
- `reduce`-এর callback: `(accumulator, currentValue, currentIndex, array)`
- `initialValue` না দিলে প্রথম element-ই accumulator হয়, আর লুপ শুরু হয় দ্বিতীয় element থেকে
- খালি array-তে `initialValue` ছাড়া `reduce` করলে `TypeError`

```javascript
const nums = [1, 2, 3, 4];
nums.map(n => n * 2);               // [2, 4, 6, 8]
nums.filter(n => n % 2 === 0);      // [2, 4]
nums.reduce((acc, n) => acc + n, 0); // 10
```

🔮 **আজ ও ভবিষ্যতে:** এই তিনটি chain করে ডেটা প্রসেস করা আধুনিক JavaScript ও React রেন্ডারিংয়ের মূল ভিত্তি।

---

## 1️⃣9️⃣ for...in আর for...of-এর পার্থক্য কী?

> 🎤 **বলুন:** `for...in` object-এর enumerable property-র **নাম (key)** ঘোরে, inherited property-ও ধরে। আর `for...of` iterable-এর **মান (value)** ঘোরে, যেমন array, string, Map, Set। Array-তে তাই আমি `for...of` ব্যবহার করি, আর object-এর জন্য `Object.entries()` সাথে `for...of`।

📌 **মূল পয়েন্ট**
- `for...in` → key (string), prototype chain-সহ
- `for...of` → value, iterable-এর জন্য
- সাধারণ object-এ `for...of` চলে না

```javascript
for (const i in ["a", "b"]) console.log(i);   // "0", "1"
for (const v of ["a", "b"]) console.log(v);   // "a", "b"
for (const [k, v] of Object.entries({ x: 1 })) console.log(k, v);
```

🔮 **আজ ও ভবিষ্যতে:** আধুনিক কোডে `Object.entries()` + `for...of` বা `map` বেশি পছন্দ করা হয়।

---

## 2️⃣0️⃣ Template literal ও tagged template কী?

> 🎤 **বলুন:** Template literal backtick দিয়ে লেখা string, যাতে `${}` দিয়ে expression বসানো যায় এবং একাধিক লাইন লেখা যায়। Tagged template-এ একটা function string-এর টুকরো ও মানগুলো আলাদাভাবে হাতে পায়, তাই সেখানে কাস্টম প্রসেসিং করা যায়। styled-components আর GraphQL-এর `gql` এভাবেই কাজ করে।

📌 **মূল পয়েন্ট**
- `${expression}` দিয়ে interpolation
- Multi-line string সরাসরি লেখা যায়
- Tagged: function প্রথম argument হিসেবে strings array আর বাকিগুলো মান পায়

```javascript
const name = "Alamin";
const msg = `Hello, ${name}! 2 + 3 = ${2 + 3}`;

function tag(strings, ...values) {
  return strings[0] + values[0].toUpperCase() + strings[1];
}
tag`Hi ${name}!`;   // "Hi ALAMIN!"
```

🔮 **আজ ও ভবিষ্যতে:** CSS-in-JS ও GraphQL লাইব্রেরিতে tagged template এখনও বহুল ব্যবহৃত।

---

## 2️⃣1️⃣ Event loop কী?

> 🎤 **বলুন:** JavaScript single-threaded, তবু async কাজ চালাতে পারে event loop-এর কারণে। Call stack খালি হলে event loop আগে **microtask queue** (Promise) পুরোটা চালায়, তারপর **task queue** (setTimeout, event) থেকে একটি করে কাজ তোলে। তাই Promise-এর callback সবসময় setTimeout-এর আগে চলে।

📌 **মূল পয়েন্ট**
- Call stack → কোড চলে
- Web/Node API → timer, network সামলায়
- Microtask queue (Promise) → **উচ্চ অগ্রাধিকার**
- Task queue (setTimeout) → পরে

```javascript
console.log("1");
setTimeout(() => console.log("2"), 0);
Promise.resolve().then(() => console.log("3"));
console.log("4");
// 1, 4, 3, 2
```

🔮 **আজ ও ভবিষ্যতে:** UI ফ্রিজ না করে ভারী কাজ ভাগ করা এবং async বাগ ডিবাগ করতে event loop বোঝা অপরিহার্য।

---

## 2️⃣2️⃣ Promise কীভাবে কাজ করে?

> 🎤 **বলুন:** Promise হলো ভবিষ্যতের কোনো ফলাফলের প্রতিশ্রুতি। এর তিনটি অবস্থা: pending, fulfilled আর rejected। সফল হলে `.then()`, ব্যর্থ হলে `.catch()`, আর শেষে সবসময় `.finally()` চলে। Chaining করে ধাপে ধাপে কাজ করা যায়, আর `Promise.all` দিয়ে একসাথে অনেকগুলো চালানো যায়।

📌 **মূল পয়েন্ট**
- অবস্থা: pending → fulfilled / rejected
- `Promise.all` → সব সফল না হলে fail
- `Promise.allSettled` → সবার ফলাফল দেয়
- `Promise.race` → প্রথম যেটা শেষ হয়

```javascript
fetch("/api/user")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err))
  .finally(() => console.log("done"));
```

🔮 **আজ ও ভবিষ্যতে:** সব আধুনিক API (fetch, Prisma, SDK) Promise ফেরত দেয়।

---

## 2️⃣3️⃣ async/await কী এবং Promise-এর চেয়ে কীভাবে ভালো?

> 🎤 **বলুন:** async/await হলো Promise-এর উপরে সিনট্যাক্স সুবিধা, যাতে async কোড synchronous-এর মতো পড়া যায়। `async` function সবসময় Promise ফেরত দেয়, আর `await` Promise-এর ফলাফলের জন্য অপেক্ষা করে। Error সামলাতে সাধারণ `try/catch` চলে, আর কোড অনেক পরিষ্কার হয়।

📌 **মূল পয়েন্ট**
- `await` শুধু `async` function-এর ভেতরে (module-এ top-level-ও চলে)
- স্বাধীন কাজ একসাথে চালাতে `Promise.all`
- `forEach`-এর ভেতরে `await` কাজ করে না

```javascript
async function load() {
  try {
    const [user, posts] = await Promise.all([getUser(), getPosts()]);
    return { user, posts };
  } catch (e) {
    console.error(e);
  }
}
```

🔮 **আজ ও ভবিষ্যতে:** Node.js, Next.js ও প্রায় সব ব্যাকএন্ড কোডে async/await-ই স্ট্যান্ডার্ড।

---

## 2️⃣4️⃣ call(), apply() ও bind()-এর পার্থক্য কী?

> 🎤 **বলুন:** তিনটাই function-এর `this` নিজে ঠিক করে দেয়। `call` সাথে সাথে function চালায় এবং argument আলাদা আলাদা নেয়। `apply` একই কাজ করে কিন্তু argument array হিসেবে নেয়। আর `bind` function চালায় না, বরং `this` বাঁধা একটি নতুন function ফেরত দেয়।

📌 **মূল পয়েন্ট**
- `call(thisArg, a, b)` → সাথে সাথে চলে
- `apply(thisArg, [a, b])` → সাথে সাথে চলে, array নেয়
- `bind(thisArg, a)` → নতুন function দেয়
- Arrow function-এ `this` বদলানো যায় না

```javascript
function hi(g) { return g + ", " + this.name; }
const u = { name: "Alamin" };
hi.call(u, "Hello");     // "Hello, Alamin"
hi.apply(u, ["Hello"]);  // একই
const f = hi.bind(u);    // নতুন function
```

🔮 **আজ ও ভবিষ্যতে:** আধুনিক কোডে arrow function আসায় `bind` কম লাগে, কিন্তু class ও পুরনো কোডে এখনও দেখা যায়।

---

## 2️⃣5️⃣ Prototypal inheritance কী?

> 🎤 **বলুন:** JavaScript-এ প্রতিটি object-এর একটি লুকানো link থাকে অন্য object-এর দিকে, যাকে prototype বলে। কোনো property না পেলে engine সেই শিকল ধরে উপরে খোঁজে, এটাই prototype chain। `class` আসলে এর উপরেই বানানো সিনট্যাক্স সুবিধা।

📌 **মূল পয়েন্ট**
- প্রতিটি object-এর `[[Prototype]]` আছে
- Property খোঁজা চলে chain ধরে, `null`-এ শেষ
- `Object.create(proto)` দিয়ে সরাসরি inherit
- `class` / `extends` = prototype-এর সিনট্যাক্স সুবিধা

```javascript
const animal = { eat() { return "eating"; } };
const dog = Object.create(animal);
dog.bark = () => "woof";
dog.eat();   // prototype থেকে আসছে
```

🔮 **আজ ও ভবিষ্যতে:** `class` ব্যবহার করলেও ভেতরে prototype-ই কাজ করে, তাই ইন্টারভিউয়ে এটি বারবার আসে।

---

## 2️⃣6️⃣ বিভিন্ন কনটেক্সটে `this` কীভাবে কাজ করে?

> 🎤 **বলুন:** `this`-এর মান নির্ভর করে function **কীভাবে call হয়েছে** তার উপর, কোথায় লেখা হয়েছে তার উপর নয়। Method call-এ object, constructor-এ নতুন instance, `call/apply/bind`-এ আমি যা দিই সেটা। কিন্তু arrow function-এ নিজস্ব `this` নেই, সে বাইরের scope থেকে নেয়।

📌 **মূল পয়েন্ট**
- Global → `window` (ব্রাউজার), module/strict-এ `undefined`
- Method call → ডটের বাঁদিকের object
- Plain function call → `undefined` (strict) বা global
- `new` → নতুন তৈরি object
- Arrow → lexical (বাইরের scope থেকে)

```javascript
const p = {
  name: "A",
  regular() { return this.name; },     // "A"
  arrow: () => this.name,              // বাইরের this, "A" নয়
};
```

🔮 **আজ ও ভবিষ্যতে:** React class component থেকে hooks-এ সরে আসায় `this`-এর জটিলতা কমেছে, কিন্তু মূল ধারণা ইন্টারভিউয়ে আজও জরুরি।

---

## 2️⃣7️⃣ JavaScript Modules (import/export) কী?

> 🎤 **বলুন:** Module হলো আলাদা ফাইলে কোড ভাগ করে `export` করা এবং অন্য ফাইলে `import` করার ব্যবস্থা। প্রতিটি module-এর নিজস্ব scope থাকে, তাই global দূষণ হয় না। Named export একাধিক হতে পারে, default export একটি। CommonJS-এর `require` runtime-এ চলে, আর ES Modules static, তাই tree-shaking সম্ভব।

📌 **মূল পয়েন্ট**
- Named export: `export const a`, import: `{ a }`
- Default export: একটি, নাম যেকোনো
- Dynamic import: `await import("./x.js")`
- ESM = static, CommonJS = dynamic (`require`)

```javascript
// math.js
export const add = (a, b) => a + b;
export default function sub(a, b) { return a - b; }

// app.js
import sub, { add } from "./math.js";
```

🔮 **আজ ও ভবিষ্যতে:** নতুন প্রজেক্ট (Next.js, Vite, Node ESM) পুরোপুরি ES Modules-এ চলে।

---

## 2️⃣8️⃣ Shallow copy ও deep copy-এর পার্থক্য কী?

> 🎤 **বলুন:** Shallow copy শুধু উপরের স্তর কপি করে, ভেতরের nested object আগের reference-ই থাকে, তাই একটা বদলালে অন্যটাও বদলায়। Deep copy পুরোটা আলাদা করে কপি করে। Spread বা `Object.assign` shallow, আর deep-এর জন্য এখন `structuredClone()` সবচেয়ে ভালো।

📌 **মূল পয়েন্ট**
- Shallow: spread, `Object.assign`, `slice`
- Deep: `structuredClone()`, lodash `cloneDeep`
- `JSON.parse(JSON.stringify())` Date, `undefined`, function, Map ভেঙে ফেলে

```javascript
const a = { n: { x: 1 } };
const s = { ...a };           // shallow
s.n.x = 99;                   // a.n.x-ও 99
const d = structuredClone(a); // deep
```

🔮 **আজ ও ভবিষ্যতে:** `structuredClone` এখন সব আধুনিক ব্রাউজার ও Node-এ আছে, তাই JSON কৌশলের দরকার কমেছে।

---

## 2️⃣9️⃣ WeakMap ও WeakSet কী এবং কখন ব্যবহার করবেন?

> 🎤 **বলুন:** WeakMap ও WeakSet-এ শুধু object key/value হিসেবে রাখা যায়, আর সেগুলো **দুর্বল reference** ধরে। অন্য কোথাও object-টির reference না থাকলে garbage collector সেটা মুছে ফেলে, ফলে memory leak হয় না। এগুলো iterate করা যায় না, `size`-ও নেই। আমি এগুলো object-এর সাথে গোপন বা cache করা ডেটা জুড়তে ব্যবহার করি।

📌 **মূল পয়েন্ট**
- Key অবশ্যই object
- Garbage collection-বান্ধব
- Iterate করা যায় না, `size` নেই
- ব্যবহার: private data, DOM node-এর metadata, visited-object ট্র্যাকিং

```javascript
const meta = new WeakMap();
let el = {};
meta.set(el, { clicks: 0 });
el = null;   // এখন meta-র entry-ও মুছে যেতে পারে
```

🔮 **আজ ও ভবিষ্যতে:** বড় অ্যাপে memory leak এড়াতে cache ও metadata রাখার সময় WeakMap একটি পেশাদার পছন্দ।

---

## 3️⃣0️⃣ Memoization কী? উদাহরণ দিন।

> 🎤 **বলুন:** Memoization হলো একটি function-এর আগের ফলাফল cache করে রাখা, যাতে একই input এলে আবার হিসাব না করে সরাসরি দেওয়া যায়। এটা শুধু pure function-এ নিরাপদ। এতে ভারী হিসাবের সময় অনেক কমে, বিনিময়ে কিছু memory লাগে।

📌 **মূল পয়েন্ট**
- Cache-এ key = argument, value = ফলাফল
- শুধু pure function-এ নিরাপদ
- ঝুঁকি: cache অনন্তভাবে বাড়তে পারে

```javascript
function memoize(fn) {
  const cache = new Map();
  return (...args) => {
    const key = JSON.stringify(args);
    if (!cache.has(key)) cache.set(key, fn(...args));
    return cache.get(key);
  };
}
const fib = memoize(n => (n < 2 ? n : fib(n - 1) + fib(n - 2)));
```

🔮 **আজ ও ভবিষ্যতে:** React-এ `useMemo`, `useCallback`, `React.memo` এই ধারণারই প্রয়োগ।
