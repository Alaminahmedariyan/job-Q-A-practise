# 🟣 JavaScript Fundamentals II — বিস্তারিত ইন্টারভিউ গাইড (বাংলা)

**টপিক:** Arrays, Objects, ES6+ & Async

> প্রতিটি প্রশ্নে ছয়টি অংশ আছে:
> 🎤 **মুখে যেভাবে বলবেন** · 📖 **বিস্তারিত ব্যাখ্যা** · 🧠 **সহজ উপমা** · 💻 **কোড** · ❓ **ফলো-আপ প্রশ্ন** · 🔮 **আজকের দিনে ও ভবিষ্যতে**

---

## 1️⃣6️⃣ Destructuring কী? Array ও object-এর উদাহরণসহ বলুন।

> 🎤 **বলুন:** জি, Destructuring হলো array বা object-এর ভেতরের মান সরাসরি আলাদা আলাদা variable-এ বের করে আনার সংক্ষিপ্ত উপায়। Array-তে এটি ক্রম (position) অনুযায়ী কাজ করে, আর object-এ property-র নাম অনুযায়ী। এর সাথে default মান, নাম বদলানো আর nested ডেটা বের করাও যায়, ফলে কোড ছোট ও পরিষ্কার হয়।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | Array destructuring | Object destructuring |
|---|---|---|
| কীসের ভিত্তিতে | Position (ক্রম) | Property-র নাম |
| বন্ধনী | `[ ]` | `{ }` |
| বাদ দেওয়া | কমা দিয়ে ফাঁক রাখা: `[a, , c]` | দরকারি নাম বেছে নেওয়া |
| নাম বদল | সরাসরি যেকোনো নাম | `{ name: userName }` |
| Default মান | `[a = 1]` | `{ age = 20 }` |
| বাকিটা ধরা | `[a, ...rest]` | `{ a, ...rest }` |

🧠 **সহজ উপমা:** একটা পার্সেল খুলে ভেতরের জিনিসগুলো আলাদা আলাদা তাকে সাজিয়ে রাখার মতো। Array হলে পার্সেলে জিনিস সাজানো থাকে ক্রম ধরে, আর object হলে প্রতিটি জিনিসের গায়ে লেবেল লাগানো থাকে।

💻 **কোড**

```javascript
// Array
const [first, second, ...others] = [10, 20, 30, 40];
// first = 10, second = 20, others = [30, 40]

// Object
const user = { name: "Alamin", city: "Sherpur", skills: { main: "Node.js" } };
const { name, age = 20, city: town } = user;
// name = "Alamin", age = 20 (default), town = "Sherpur"

// Nested
const { skills: { main } } = user;   // main = "Node.js"

// Swap
let a = 1, b = 2;
[a, b] = [b, a];                     // a = 2, b = 1

// Function parameter
function greet({ name, role = "user" }) {
  return `${name} (${role})`;
}
```

❓ **ফলো-আপ:** "মান `undefined` হলে কী হয়?" → তখন default মান বসে। কিন্তু মান `null` হলে default বসে না।

🔮 **আজ ও ভবিষ্যতে:** `const [state, setState] = useState()` আর props destructuring প্রতিদিনের React কোড। ইন্টারভিউয়ে এটি বলতে পারা মানে আধুনিক JavaScript-এর সাথে স্বচ্ছন্দ।

---

## 1️⃣7️⃣ Spread ও Rest অপারেটর কী এবং কীভাবে ব্যবহার হয়?

> 🎤 **বলুন:** দুটোরই চিহ্ন `...`, কিন্তু কাজ উল্টো। Spread একটা array বা object-কে ছড়িয়ে দেয়, আর Rest অনেকগুলো মানকে একটা array বা object-এ জড়ো করে। Spread দিয়ে আমি copy ও merge করি, আর Rest দিয়ে function-এ অজানা সংখ্যক argument ধরি। মনে রাখার বিষয়, Spread-এর copy shallow।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | Spread | Rest |
|---|---|---|
| কাজ | ছড়িয়ে দেয় | জড়ো করে |
| কোথায় বসে | call-এ, array/object literal-এ | parameter বা destructuring-এ |
| ব্যবহার | copy, merge, argument পাঠানো | variable সংখ্যক argument ধরা |
| নিয়ম | যেকোনো জায়গায় চলে | **সবসময় শেষে** থাকতে হবে |

🧠 **সহজ উপমা:** Spread হলো একটা ব্যাগ উপুড় করে সব জিনিস টেবিলে ছড়িয়ে দেওয়া। Rest হলো টেবিলে পড়ে থাকা বাকি সব জিনিস একটা নতুন ব্যাগে তুলে নেওয়া।

💻 **কোড**

```javascript
// Spread
const merged = [...[1, 2], ...[3, 4]];            // [1, 2, 3, 4]
const user2 = { ...user, role: "admin" };         // copy + নতুন property
Math.max(...[5, 9, 2]);                           // 9

// Rest
const sum = (...nums) => nums.reduce((a, b) => a + b, 0);
sum(1, 2, 3);                                     // 6

const [head, ...tail] = [1, 2, 3];                // tail = [2, 3]
const { id, ...rest } = { id: 1, a: 2, b: 3 };    // rest = { a: 2, b: 3 }
```

⚠️ **ফাঁদ (shallow copy):**

```javascript
const a = { info: { x: 1 } };
const b = { ...a };
b.info.x = 99;
console.log(a.info.x); // 99, কারণ nested object একই reference
```

❓ **ফলো-আপ:** "Rest parameter আর `arguments`-এর পার্থক্য?" → Rest সত্যিকারের array, আর `arguments` array-এর মতো দেখতে object এবং arrow function-এ নেই।

🔮 **আজ ও ভবিষ্যতে:** React state immutable ভাবে আপডেট করতে spread সবচেয়ে বেশি ব্যবহৃত প্যাটার্ন।

---

## 1️⃣8️⃣ map(), filter() ও reduce()-এর পার্থক্য কী?

> 🎤 **বলুন:** তিনটাই array method, এবং মূল array না বদলে নতুন ফলাফল দেয়। `map` প্রতিটি element রূপান্তর করে একই দৈর্ঘ্যের নতুন array দেয়। `filter` শর্ত মেলা element দিয়ে ছোট array দেয়। আর `reduce` পুরো array থেকে একটিমাত্র মান বের করে, যেমন যোগফল বা object।

📖 **বিস্তারিত ব্যাখ্যা**

| Method | কাজ | Return | দৈর্ঘ্য |
|---|---|---|---|
| `map` | প্রতিটি element রূপান্তর | নতুন array | একই |
| `filter` | শর্ত মেলা element বাছাই | নতুন array | কম বা সমান |
| `reduce` | সবকিছু একটি মানে সংক্ষেপ | যেকোনো একটি মান | নেই |

**`reduce`-এর গঠন:**

```javascript
array.reduce(callback(accumulator, currentValue, currentIndex, array), initialValue);
```

- `accumulator`: আগের ধাপের ফলাফল (প্রথম ধাপে `initialValue`)
- `currentValue`: বর্তমান element
- `currentIndex` (ঐচ্ছিক): বর্তমান element-এর index
- `array` (ঐচ্ছিক): যে array-তে `reduce` চালানো হয়েছে
- `initialValue` (ঐচ্ছিক): না দিলে প্রথম element-ই accumulator হয় এবং লুপ শুরু হয় **দ্বিতীয় element থেকে**

⚠️ খালি array-তে `initialValue` ছাড়া `reduce` করলে `TypeError` আসে। তাই সবসময় `initialValue` দেওয়া নিরাপদ।

🧠 **সহজ উপমা:** কারখানার সারি: `map` হলো প্রতিটি পণ্যে রঙ করা, `filter` হলো ত্রুটিপূর্ণ পণ্য বাদ দেওয়া, আর `reduce` হলো সব পণ্য একটা বাক্সে প্যাক করে মোট হিসাব বের করা।

💻 **কোড**

```javascript
const nums = [1, 2, 3, 4, 5];

nums.map(n => n * 2);                  // [2, 4, 6, 8, 10]
nums.filter(n => n % 2 === 0);         // [2, 4]
nums.reduce((acc, n) => acc + n, 0);   // 15

// Chain
const total = [
  { name: "A", price: 100, inStock: true },
  { name: "B", price: 50, inStock: false },
  { name: "C", price: 70, inStock: true },
]
  .filter(p => p.inStock)
  .map(p => p.price)
  .reduce((sum, price) => sum + price, 0);   // 170

// reduce দিয়ে গণনা
["a", "b", "a"].reduce((acc, ch) => {
  acc[ch] = (acc[ch] || 0) + 1;
  return acc;
}, {});                                       // { a: 2, b: 1 }
```

❓ **ফলো-আপ:** "`forEach` আর `map`-এর পার্থক্য?" → `forEach` কিছু ফেরত দেয় না (`undefined`), আর `map` নতুন array ফেরত দেয়।

🔮 **আজ ও ভবিষ্যতে:** এই তিনটি chain করে ডেটা প্রসেস করা আধুনিক JavaScript ও React লিস্ট রেন্ডারিংয়ের মূল ভিত্তি।

---

## 1️⃣9️⃣ for...in আর for...of লুপের পার্থক্য কী?

> 🎤 **বলুন:** `for...in` object-এর enumerable property-র **নাম (key)** ঘোরে, এমনকি inherited property-ও ধরে। আর `for...of` iterable-এর **মান (value)** ঘোরে, যেমন array, string, Map, Set। তাই array-তে আমি `for...of` ব্যবহার করি, আর object-এর জন্য `Object.entries()` সাথে `for...of`।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | `for...in` | `for...of` |
|---|---|---|
| কী পাওয়া যায় | Key (সবসময় string) | Value |
| কোথায় চলে | Object (এবং array, তবে প্রস্তাবিত নয়) | Iterable (Array, String, Map, Set) |
| Prototype chain | ধরে (inherited property-ও) | প্রযোজ্য নয় |
| সাধারণ object-এ | চলে | চলে না (`TypeError`) |

🧠 **সহজ উপমা:** `for...in` হলো ঘরের দরজার নামফলক পড়া, আর `for...of` হলো প্রতিটি ঘরের ভেতরে কী আছে সেটা দেখা।

💻 **কোড**

```javascript
const arr = ["a", "b"];
for (const i in arr) console.log(i);   // "0", "1" (string index)
for (const v of arr) console.log(v);   // "a", "b"

for (const ch of "Hi") console.log(ch); // "H", "i"

const obj = { x: 1, y: 2 };
for (const k in obj) console.log(k);                        // "x", "y"
for (const [k, v] of Object.entries(obj)) console.log(k, v); // x 1, y 2
// for (const v of obj) {}  // TypeError: obj is not iterable
```

❓ **ফলো-আপ:** "Array-তে `for...in` কেন এড়ানো উচিত?" → index string হিসেবে আসে, ক্রমের নিশ্চয়তা নেই, আর array-তে যোগ করা অতিরিক্ত property বা prototype-এর enumerable property-ও চলে আসতে পারে।

🔮 **আজ ও ভবিষ্যতে:** আধুনিক কোডে `Object.entries()` + `for...of` বা array method বেশি পছন্দ করা হয়।

---

## 2️⃣0️⃣ Template literal ও tagged template কী?

> 🎤 **বলুন:** Template literal হলো backtick দিয়ে লেখা string, যাতে `${}` দিয়ে যেকোনো expression বসানো যায় এবং একাধিক লাইন সরাসরি লেখা যায়। Tagged template-এ একটা function string-এর টুকরো ও মানগুলো আলাদাভাবে হাতে পায়, ফলে কাস্টম প্রসেসিং করা যায়। styled-components আর GraphQL-এর `gql` এভাবেই কাজ করে।

📖 **বিস্তারিত ব্যাখ্যা**

- **সাধারণ template literal:** backtick (`` ` ``), `${expression}`, multi-line সমর্থন
- **Tagged template:** function-এর নামের পরে সরাসরি template লেখা হয়। Function প্রথম argument হিসেবে **strings-এর array** আর বাকি argument হিসেবে **মানগুলো** পায়
- ব্যবহার: HTML/SQL escaping, styled-components, GraphQL, i18n

🧠 **সহজ উপমা:** ফর্ম-লেটারে ফাঁকা ঘর রাখা থাকে, নাম ও তারিখ বসালেই চিঠি তৈরি। Tagged template হলো এমন একজন সহকারী, যে ফাঁকা ঘর পূরণের আগে প্রতিটি মান যাচাই বা সাজিয়ে নেয়।

💻 **কোড**

```javascript
const name = "Alamin";

// সাধারণ
const msg = `Hello, ${name}!
2 + 3 = ${2 + 3}`;

// Tagged
function highlight(strings, ...values) {
  return strings.reduce(
    (out, str, i) => out + str + (values[i] !== undefined ? `[${values[i]}]` : ""),
    ""
  );
}
highlight`Hi ${name}, you are ${25} years old`;
// "Hi [Alamin], you are [25] years old"
```

❓ **ফলো-আপ:** "Tagged template-এ `strings` কী ধরনের?" → string-এর array, যার একটি `raw` property-ও আছে (escape না করা মূল text)।

🔮 **আজ ও ভবিষ্যতে:** CSS-in-JS ও GraphQL লাইব্রেরিতে tagged template এখনও বহুল ব্যবহৃত।

---

## 2️⃣1️⃣ Event loop কী?

> 🎤 **বলুন:** JavaScript single-threaded, অর্থাৎ একবারে একটাই কাজ করে, তবু async কাজ চালাতে পারে event loop-এর কারণে। Call stack খালি হলে event loop আগে **microtask queue** (Promise) পুরোটা চালায়, তারপর **task queue** (setTimeout, event) থেকে একটি করে কাজ তোলে। তাই Promise-এর callback সবসময় `setTimeout`-এর আগে চলে।

📖 **বিস্তারিত ব্যাখ্যা**

| অংশ | কাজ |
|---|---|
| Call stack | বর্তমানে চলমান কোড |
| Web APIs / Node APIs | timer, network, DOM event সামলায় (JavaScript-এর বাইরে) |
| Microtask queue | Promise `.then`, `queueMicrotask`, **উচ্চ অগ্রাধিকার** |
| Task (macrotask) queue | `setTimeout`, `setInterval`, UI event |
| Event loop | stack খালি হলে queue থেকে কাজ তুলে stack-এ দেয় |

**ক্রম:** stack খালি → **সব microtask শেষ** → **একটি** task → আবার microtask → ...

🧠 **সহজ উপমা:** একজন একা ওয়েটার (stack)। অর্ডার নিয়ে রান্নাঘরে (Web API) দিয়ে অন্য টেবিল সামলায়। খাবার তৈরি হলে ভিআইপি লাইনের (microtask) অর্ডার আগে পরিবেশন করে, তারপর সাধারণ লাইনের (task) একটি করে।

💻 **কোড**

```javascript
console.log("1");                              // sync
setTimeout(() => console.log("2"), 0);         // task queue
Promise.resolve().then(() => console.log("3")); // microtask
console.log("4");                              // sync

// আউটপুট: 1, 4, 3, 2
```

❓ **ফলো-আপ:** "`setTimeout(fn, 0)` সাথে সাথে চলে?" → না। এটি task queue-তে যায়, stack ও সব microtask শেষ হলে তবেই চলে।

🔮 **আজ ও ভবিষ্যতে:** UI ফ্রিজ না করে ভারী কাজ ভাগ করা এবং async বাগ ডিবাগ করতে event loop বোঝা অপরিহার্য। Node.js-এও একই ধারণা, সাথে কিছু অতিরিক্ত phase আছে।

---

## 2️⃣2️⃣ Promise কীভাবে কাজ করে?

> 🎤 **বলুন:** Promise হলো ভবিষ্যতের কোনো ফলাফলের প্রতিশ্রুতি। এর তিনটি অবস্থা: pending, fulfilled আর rejected। সফল হলে `.then()`, ব্যর্থ হলে `.catch()`, আর শেষে সবসময় `.finally()` চলে। Chaining করে ধাপে ধাপে কাজ করা যায়, আর `Promise.all` দিয়ে একসাথে অনেকগুলো চালানো যায়।

📖 **বিস্তারিত ব্যাখ্যা**

**অবস্থা:** `pending` (অপেক্ষমাণ) → `fulfilled` (সফল) অথবা `rejected` (ব্যর্থ)। একবার settle হলে আর বদলায় না।

| Method | আচরণ |
|---|---|
| `Promise.all([...])` | সব সফল হলে ফলাফলের array, একটি ব্যর্থ হলেই পুরোটা ব্যর্থ |
| `Promise.allSettled([...])` | সবার ফলাফল দেয়, সফল বা ব্যর্থ নির্বিশেষে |
| `Promise.race([...])` | যেটা আগে শেষ হয় (সফল বা ব্যর্থ) |
| `Promise.any([...])` | প্রথম **সফল**টি, সব ব্যর্থ হলে error |

🧠 **সহজ উপমা:** রেস্টুরেন্টে অর্ডার দিলে টোকেন পাওয়া। খাবার তৈরি না হওয়া পর্যন্ত টোকেন "pending"। খাবার এলে "fulfilled", আর খাবার শেষ হয়ে গেলে "rejected"।

💻 **কোড**

```javascript
const wait = (ms, v) => new Promise(res => setTimeout(() => res(v), ms));

fetch("/api/user")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err))
  .finally(() => console.log("done"));

Promise.all([wait(100, "a"), wait(200, "b")]).then(console.log); // ["a", "b"]

const p = new Promise((resolve, reject) => {
  const ok = true;
  ok ? resolve("সফল") : reject(new Error("ব্যর্থ"));
});
```

❓ **ফলো-আপ:** "`.then`-এর ভেতরে error হলে কী হয়?" → chain-এর পরের `.catch` সেটা ধরে।

🔮 **আজ ও ভবিষ্যতে:** সব আধুনিক API (fetch, Prisma, বিভিন্ন SDK) Promise ফেরত দেয়।

---

## 2️⃣3️⃣ async/await কী এবং Promise-এর চেয়ে কীভাবে ভালো?

> 🎤 **বলুন:** async/await হলো Promise-এর উপরে সিনট্যাক্স সুবিধা, যাতে async কোড synchronous-এর মতো উপর থেকে নিচে পড়া যায়। `async` function সবসময় Promise ফেরত দেয়, আর `await` Promise-এর ফলাফলের জন্য অপেক্ষা করে। Error সামলাতে সাধারণ `try/catch` চলে, তাই `.then` chain-এর জটিলতা কমে।

📖 **বিস্তারিত ব্যাখ্যা**

- `async` function সবসময় Promise ফেরত দেয়
- `await` শুধু `async` function-এর ভেতরে চলে (ES module-এ top-level `await`-ও চলে)
- `await` পুরো প্রোগ্রাম থামায় না, শুধু ওই function-এর বাকি অংশ থামায়

**সাধারণ ভুল:**
1. স্বাধীন কাজ পরপর `await` করা (ধীর), এর বদলে `Promise.all`
2. `forEach`-এর ভেতরে `await` (অপেক্ষা করে না), এর বদলে `for...of` বা `Promise.all(map(...))`
3. `try/catch` ভুলে যাওয়া

🧠 **সহজ উপমা:** Promise chain হলো নির্দেশনা ছেঁড়া ছেঁড়া কাগজে লেখা, "এটা শেষ হলে ওটা করো"। async/await হলো একই নির্দেশনা একটানা একটা পাতায় সোজা লেখা।

💻 **কোড**

```javascript
// Promise chain
function loadOld() {
  return getUser().then(u => getPosts(u.id)).then(posts => posts.length);
}

// async/await
async function load() {
  try {
    const user = await getUser();
    const posts = await getPosts(user.id);
    return posts.length;
  } catch (e) {
    console.error(e);
  }
}

// স্বাধীন কাজ একসাথে
async function loadAll() {
  const [user, settings] = await Promise.all([getUser(), getSettings()]);
  return { user, settings };
}
```

❓ **ফলো-আপ:** "`await` ছাড়া async function call করলে কী পাই?" → একটি Promise, তার ভেতরের মান নয়।

🔮 **আজ ও ভবিষ্যতে:** Node.js, Next.js ও প্রায় সব ব্যাকএন্ড কোডে async/await-ই স্ট্যান্ডার্ড।

---

## 2️⃣4️⃣ call(), apply() ও bind()-এর পার্থক্য কী?

> 🎤 **বলুন:** তিনটাই function-এর `this` নিজে ঠিক করে দেয়। `call` সাথে সাথে function চালায় এবং argument আলাদা আলাদা নেয়। `apply` একই কাজ করে কিন্তু argument array হিসেবে নেয়। আর `bind` function চালায় না, বরং `this` বাঁধা একটি নতুন function ফেরত দেয়, যা পরে চালানো যায়।

📖 **বিস্তারিত ব্যাখ্যা**

| Method | কখন চলে | Argument | Return |
|---|---|---|---|
| `call(thisArg, a, b)` | সাথে সাথে | আলাদা আলাদা | function-এর ফলাফল |
| `apply(thisArg, [a, b])` | সাথে সাথে | array আকারে | function-এর ফলাফল |
| `bind(thisArg, a)` | পরে (নতুন function) | আলাদা আলাদা (partial) | নতুন function |

মনে রাখার কৌশল: **A**pply = **A**rray, **C**all = **C**omma, **B**ind = **B**ound function।

🧠 **সহজ উপমা:** একটা ফোন (function), সিম বদলানো মানে `this` বদলানো। `call` মানে সিম লাগিয়ে এখনই কল করা। `bind` মানে সিম লাগানো একটা নতুন ফোন বানিয়ে রাখা, পরে যখন ইচ্ছা কল করা।

💻 **কোড**

```javascript
function intro(greeting, punct) {
  return `${greeting}, ${this.name}${punct}`;
}
const user = { name: "Alamin" };

intro.call(user, "Hello", "!");     // "Hello, Alamin!"
intro.apply(user, ["Hello", "!"]);  // "Hello, Alamin!"

const bound = intro.bind(user, "Hi");
bound("?");                         // "Hi, Alamin?"

// ক্লাসিক ব্যবহার: setTimeout-এ this হারানো ঠেকানো
const counter = {
  n: 0,
  start() { setInterval(function () { this.n++; }.bind(this), 1000); },
};
```

❓ **ফলো-আপ:** "Arrow function-এ `call` দিয়ে `this` বদলানো যায়?" → না, arrow function-এর `this` lexical, তাই `call/apply/bind` সেটা বদলাতে পারে না।

🔮 **আজ ও ভবিষ্যতে:** Arrow function আসায় `bind` কম লাগে, কিন্তু class ও পুরনো কোডে এখনও দেখা যায়।

---

## 2️⃣5️⃣ Prototypal inheritance কী?

> 🎤 **বলুন:** JavaScript-এ প্রতিটি object-এর একটি লুকানো link থাকে অন্য object-এর দিকে, যাকে prototype বলে। কোনো property বা method না পেলে engine সেই শিকল ধরে উপরে খোঁজে, এটাই prototype chain। `class` আসলে এরই উপর বানানো সিনট্যাক্স সুবিধা, ভেতরে প্রটোটাইপই কাজ করে।

📖 **বিস্তারিত ব্যাখ্যা**

- প্রতিটি object-এর একটি `[[Prototype]]` আছে (`Object.getPrototypeOf(obj)` দিয়ে দেখা যায়)
- Property খোঁজার ক্রম: নিজের → prototype → তার prototype → ... → `null`
- `__proto__` হলো object-এর prototype-এর পুরনো অ্যাক্সেসর, আর `prototype` হলো **function**-এর property, যা `new` করা object-এর prototype হয়
- `hasOwnProperty()` / `Object.hasOwn()` দিয়ে নিজস্ব property বোঝা যায়

🧠 **সহজ উপমা:** পারিবারিক উত্তরাধিকার। কোনো জিনিস তোমার কাছে না থাকলে বাবার কাছে খোঁজো, সেখানে না থাকলে দাদুর কাছে, এভাবে শেষ পর্যন্ত।

💻 **কোড**

```javascript
const animal = { eat() { return "eating"; } };
const dog = Object.create(animal);   // dog-এর prototype = animal
dog.bark = () => "woof";

dog.bark();                          // নিজের
dog.eat();                           // prototype থেকে
Object.getPrototypeOf(dog) === animal; // true

// Constructor function
function Person(name) { this.name = name; }
Person.prototype.hello = function () { return "Hi " + this.name; };
new Person("A").hello();             // "Hi A"

// class (একই জিনিস, নতুন সিনট্যাক্স)
class Student extends Person {
  study() { return this.name + " is studying"; }
}
```

❓ **ফলো-আপ:** "`prototype` আর `__proto__`-এর পার্থক্য?" → `prototype` function-এর property, `__proto__` প্রতিটি object-এর link যা সেই prototype-কে দেখায়।

🔮 **আজ ও ভবিষ্যতে:** `class` ব্যবহার করলেও ভেতরে prototype-ই কাজ করে, তাই ইন্টারভিউয়ে এটি বারবার আসে।

---

## 2️⃣6️⃣ বিভিন্ন কনটেক্সটে `this` কীভাবে কাজ করে?

> 🎤 **বলুন:** `this`-এর মান নির্ভর করে function **কীভাবে call হয়েছে** তার উপর, কোথায় লেখা হয়েছে তার উপর নয়। Method call-এ object, constructor-এ নতুন instance, `call/apply/bind`-এ আমি যা দিই সেটা। কিন্তু arrow function-এ নিজস্ব `this` নেই, সে বাইরের scope থেকে নেয়।

📖 **বিস্তারিত ব্যাখ্যা**

| কনটেক্সট | `this` কী হয় |
|---|---|
| Global (ব্রাউজার) | `window` (module বা strict mode-এ `undefined`) |
| Method call `obj.fn()` | `obj` (ডটের বাঁদিকের object) |
| Plain function call `fn()` | `undefined` (strict) / global (non-strict) |
| Constructor `new Fn()` | নতুন তৈরি object |
| `call / apply / bind` | আপনার দেওয়া মান |
| Arrow function | বাইরের scope-এর `this` (lexical) |
| DOM event handler (regular function) | যে element-এ event ঘটেছে |

**Normal vs Arrow function:**

| বৈশিষ্ট্য | Normal function | Arrow function |
|---|---|---|
| `this` | Dynamic, call site ঠিক করে | Lexical, বাইরের scope থেকে |
| Method হিসেবে | যে object call করছে সেটা | বাইরের `this`, object নয় |
| Constructor (`new`) | চলে | চলে না |
| `arguments` | আছে | নেই |

🧠 **সহজ উপমা:** `this` হলো "আমি" শব্দটির মতো। কে বলছে, তার উপর অর্থ বদলায়। কিন্তু arrow function হলো এমন একজন, যে সবসময় নিজের বদলে যে ঘরে জন্মেছে সেই ঘরের "আমি"-কে ব্যবহার করে।

💻 **কোড**

```javascript
const person = {
  name: "Alamin",
  regular() { return this.name; },       // "Alamin"
  arrow: () => this.name,                // বাইরের this, "Alamin" নয়
  delayed() {
    setTimeout(() => console.log(this.name), 100);   // "Alamin" (arrow lexical)
  },
};

const fn = person.regular;
fn();                                    // this হারিয়ে গেছে (undefined/global)

function Car(model) { this.model = model; }
new Car("X").model;                      // "X"
```

❓ **ফলো-আপ:** "Method আলাদা variable-এ নিলে `this` হারায় কেন?" → কারণ তখন আর `obj.fn()` ভাবে call হচ্ছে না, call site বদলে গেছে। সমাধান: `bind` বা arrow function।

🔮 **আজ ও ভবিষ্যতে:** React hooks আসায় `this`-এর জটিলতা কমেছে, কিন্তু মূল ধারণা ইন্টারভিউতে আজও জরুরি।

---

## 2️⃣7️⃣ JavaScript Modules (import/export) কী?

> 🎤 **বলুন:** Module হলো কোড আলাদা ফাইলে ভাগ করে `export` করা এবং অন্য ফাইলে `import` করার ব্যবস্থা। প্রতিটি module-এর নিজস্ব scope থাকে, তাই global দূষণ হয় না। একটি ফাইলে একাধিক named export এবং একটি default export থাকতে পারে। CommonJS-এর `require` runtime-এ চলে, আর ES Modules static, তাই tree-shaking সম্ভব।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | ES Modules (ESM) | CommonJS (CJS) |
|---|---|---|
| সিনট্যাক্স | `import` / `export` | `require()` / `module.exports` |
| লোড | Static (আগে থেকেই বিশ্লেষণ) | Dynamic (runtime-এ) |
| Tree-shaking | সম্ভব | কঠিন |
| `this` (top-level) | `undefined` | `module.exports` |
| ডিফল্ট mode | Strict | Non-strict |

- **Named export:** একাধিক, import-এ ঠিক নামটাই লাগে (`{ add }`)
- **Default export:** ফাইল-প্রতি একটি, import-এ যেকোনো নাম
- **Live binding:** import করা মান মূলটির সাথে সংযুক্ত থাকে
- **Dynamic import:** `const m = await import("./x.js")` (শর্ত অনুযায়ী লোড)
- Node.js-এ ESM চালাতে `package.json`-এ `"type": "module"` বা `.mjs` ফাইল

🧠 **সহজ উপমা:** আলাদা আলাদা টুলবক্স। যেটা দরকার সেটাই অন্য বাক্স থেকে চেয়ে আনো (`import`), আর নিজের বাক্সে যা অন্যকে দিতে চাও তা বাইরে রাখো (`export`)।

💻 **কোড**

```javascript
// math.js
export const add = (a, b) => a + b;
export const PI = 3.14;
export default function sub(a, b) { return a - b; }

// app.js
import sub, { add, PI as pi } from "./math.js";
import * as math from "./math.js";     // সব একসাথে

const { default: lazy } = await import("./math.js"); // dynamic
```

❓ **ফলো-আপ:** "Tree-shaking কী?" → ব্যবহার না হওয়া export bundle থেকে বাদ দেওয়া, ESM static বলেই এটা সম্ভব।

🔮 **আজ ও ভবিষ্যতে:** নতুন প্রজেক্ট (Next.js, Vite, Node ESM) পুরোপুরি ES Modules-এ চলে।

---

## 2️⃣8️⃣ Shallow copy ও deep copy-এর পার্থক্য কী?

> 🎤 **বলুন:** Shallow copy শুধু উপরের স্তর কপি করে, ভেতরের nested object আগের reference-ই থাকে, তাই একটা বদলালে অন্যটাও বদলে যায়। Deep copy পুরোটা আলাদা করে কপি করে। Spread বা `Object.assign` shallow, আর deep-এর জন্য এখন `structuredClone()` সবচেয়ে ভালো।

📖 **বিস্তারিত ব্যাখ্যা**

| পদ্ধতি | ধরন | সীমাবদ্ধতা |
|---|---|---|
| Spread `{ ...obj }`, `[...arr]` | Shallow | nested শেয়ার হয় |
| `Object.assign({}, obj)` | Shallow | nested শেয়ার হয় |
| `arr.slice()` | Shallow | nested শেয়ার হয় |
| `structuredClone(obj)` | **Deep** | function, DOM node কপি হয় না |
| `JSON.parse(JSON.stringify(obj))` | Deep (সীমিত) | `Date`, `undefined`, function, `Map`, `Set` নষ্ট হয় |
| lodash `cloneDeep` | Deep | বাইরের লাইব্রেরি |

🧠 **সহজ উপমা:** Shallow copy হলো বইয়ের ফটোকপি যেখানে ছবির পাতাগুলো মূল বইয়ের সাথে আঠা দিয়ে লাগানো। Deep copy হলো পুরো বই নতুন করে ছাপানো।

💻 **কোড**

```javascript
const original = { name: "A", address: { city: "Sherpur" } };

const shallow = { ...original };
shallow.address.city = "Dhaka";
console.log(original.address.city);   // "Dhaka" (বদলে গেল!)

const deep = structuredClone(original);
deep.address.city = "Sylhet";
console.log(original.address.city);   // "Dhaka" (অক্ষত)

// JSON কৌশলের সমস্যা
JSON.parse(JSON.stringify({ d: new Date(), u: undefined, f() {} }));
// { d: "2026-...", } (Date string হয়ে গেছে, u ও f হারিয়ে গেছে)
```

❓ **ফলো-আপ:** "`structuredClone` কী কপি করতে পারে না?" → function এবং DOM node।

🔮 **আজ ও ভবিষ্যতে:** `structuredClone` এখন সব আধুনিক ব্রাউজার ও Node-এ আছে, তাই JSON কৌশলের দরকার কমেছে।

---

## 2️⃣9️⃣ WeakMap ও WeakSet কী এবং কখন ব্যবহার করবেন?

> 🎤 **বলুন:** WeakMap ও WeakSet-এ শুধু object রাখা যায়, আর সেগুলো **দুর্বল reference** ধরে। অন্য কোথাও object-টির reference না থাকলে garbage collector সেটা মুছে ফেলে, ফলে memory leak হয় না। এগুলো iterate করা যায় না, `size`-ও নেই। আমি এগুলো object-এর সাথে গোপন বা cache করা ডেটা জুড়তে ব্যবহার করি।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | `Map` / `Set` | `WeakMap` / `WeakSet` |
|---|---|---|
| Key কী হতে পারে | যেকোনো মান | শুধু object |
| Reference | শক্ত (strong) | দুর্বল (weak) |
| Garbage collection | key থাকলে মুছে না | অন্য reference না থাকলে মুছে যায় |
| Iterate | করা যায় | করা যায় না |
| `size` | আছে | নেই |

**ব্যবহার:**
1. Object-এর private ডেটা রাখা
2. DOM node-এর metadata বা cache (node মুছলে ডেটাও মুছবে)
3. WeakSet দিয়ে ইতিমধ্যে দেখা object ট্র্যাক করা (যেমন circular reference ঠেকানো)

🧠 **সহজ উপমা:** Map হলো এমন নোটবই যা কাউকে কখনো ভোলে না। WeakMap হলো এমন নোটবই, যেখানে কেউ শহর ছেড়ে চলে গেলে তার নামও আপনা-আপনি মুছে যায়।

💻 **কোড**

```javascript
const meta = new WeakMap();

let el = { id: 1 };
meta.set(el, { clicks: 0 });
meta.get(el).clicks++;       // 1
el = null;                   // এখন meta-র entry-ও garbage collect হতে পারে

// WeakSet
const visited = new WeakSet();
function walk(node) {
  if (visited.has(node)) return;   // circular reference থেকে বাঁচা
  visited.add(node);
}

// WeakMap দিয়ে private data
const priv = new WeakMap();
class User {
  constructor(pass) { priv.set(this, { pass }); }
  check(p) { return priv.get(this).pass === p; }
}
```

❓ **ফলো-আপ:** "WeakMap iterate করা যায় না কেন?" → কারণ garbage collector কখন entry মুছবে তা অনির্দিষ্ট, তাই তালিকা স্থির হতে পারে না।

🔮 **আজ ও ভবিষ্যতে:** বড় অ্যাপে memory leak এড়াতে cache ও metadata রাখার সময় WeakMap একটি পেশাদার পছন্দ।

---

## 3️⃣0️⃣ Memoization কী? উদাহরণ দিন।

> 🎤 **বলুন:** Memoization হলো একটি function-এর আগের ফলাফল cache করে রাখা, যাতে একই input এলে আবার হিসাব না করে সরাসরি সেই ফলাফল দেওয়া যায়। এটা শুধু pure function-এ নিরাপদ। এতে ভারী হিসাবের সময় অনেক কমে, বিনিময়ে কিছু memory লাগে।

📖 **বিস্তারিত ব্যাখ্যা**

- Cache-এর key হয় argument, value হয় ফলাফল
- আগে cache দেখা হয়, থাকলে সেটা ফেরত, না থাকলে হিসাব করে cache-এ রাখা হয়
- **শর্ত:** function pure হতে হবে (একই input → একই output, side effect নেই)
- **ঝুঁকি:** cache অনির্দিষ্টভাবে বাড়তে পারে (সীমা বা LRU দরকার), আর `JSON.stringify` key বানানো সব ডেটার জন্য নিরাপদ নয়

🧠 **সহজ উপমা:** গণিতের গুণ-নামতা মুখস্থ রাখা। প্রতিবার হিসাব না করে মুখস্থ উত্তরটা বলে দেওয়া।

💻 **কোড**

```javascript
function memoize(fn) {
  const cache = new Map();
  return function (...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);   // cache hit
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

const slowSquare = n => { /* ভারী হিসাব */ return n * n; };
const fastSquare = memoize(slowSquare);
fastSquare(9);  // হিসাব হলো
fastSquare(9);  // cache থেকে এলো

// Fibonacci: সময় O(2^n) থেকে O(n)
const fib = memoize(n => (n < 2 ? n : fib(n - 1) + fib(n - 2)));
fib(40);
```

❓ **ফলো-আপ:** "Memoization আর caching-এর পার্থক্য?" → Memoization হলো function-এর ফলাফল argument ধরে cache করা, একটি নির্দিষ্ট ধরনের caching।

🔮 **আজ ও ভবিষ্যতে:** React-এর `useMemo`, `useCallback` ও `React.memo` এই ধারণারই প্রয়োগ, তাই প্রোডাকশনে পারফরম্যান্স অপটিমাইজেশনে এটি কাজে লাগে।

---

## ✅ ইন্টারভিউয়ের আগে শেষ মুহূর্তের চেকলিস্ট

- [ ] Destructuring ও spread/rest-এর পার্থক্য উদাহরণসহ বলতে পারি
- [ ] `map`, `filter`, `reduce` এবং `reduce`-এর `initialValue`-এর আচরণ জানি
- [ ] Event loop-এর microtask বনাম task ক্রম ব্যাখ্যা করতে পারি
- [ ] Promise, async/await এবং `Promise.all`-এর ব্যবহার বুঝিয়ে বলতে পারি
- [ ] `this`-এর বিভিন্ন কনটেক্সট এবং `call/apply/bind` বলতে পারি
- [ ] Shallow বনাম deep copy এবং `structuredClone` জানি
