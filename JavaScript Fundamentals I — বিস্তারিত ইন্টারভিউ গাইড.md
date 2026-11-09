# 🟣 JavaScript Fundamentals I — বিস্তারিত ইন্টারভিউ গাইড

**টপিক:** Variables, Data Types, Functions & Scope

> প্রতিটি প্রশ্নে পাঁচটি অংশ আছে:
> 🎤 **মুখে যেভাবে বলবেন** · 📖 **বিস্তারিত ব্যাখ্যা** · 💻 **কোড উদাহরণ** · ❓ **ফলো-আপ প্রশ্ন** · 🔮 **আজকের দিনে ও ভবিষ্যতে**

---

## 1️⃣ var, let ও const-এর পার্থক্য কী?

> 🎤 **বলুন:** জি, তিনটাই variable declare করার উপায়। পার্থক্য scope, hoisting আর reassign-এর নিয়মে। var function-scoped, আর let ও const block-scoped। const-এ আবার মান assign করা যায় না, তবে object বা array-এর ভেতরের মান বদলানো যায়। আমি সবসময় const দিয়ে শুরু করি, দরকার হলে let ব্যবহার করি, আর var এড়িয়ে চলি।

📖 **বিস্তারিত ব্যাখ্যা**

| বৈশিষ্ট্য | `var` | `let` | `const` |
|---|---|---|---|
| Scope | Function | Block | Block |
| Hoisting | হয়, মান `undefined` | হয়, TDZ-তে থাকে | হয়, TDZ-তে থাকে |
| Redeclare | চলে | চলে না | চলে না |
| Reassign | চলে | চলে | চলে না |
| শুরুতে মান দেওয়া বাধ্যতামূলক? | না | না | হ্যাঁ |
| Global-এ `window` property হয়? | হ্যাঁ | না | না |

গুরুত্বপূর্ণ কথা: `const` মানে মান immutable নয়, বরং binding reassign করা যায় না। Object বা array-এর ভেতরের মান বদলানো যায়।

💻 **কোড**

```javascript
function demo() {
  if (true) {
    var a = 1;   // function scope
    let b = 2;   // block scope
    const c = 3; // block scope
  }
  console.log(a); // 1
  console.log(b); // ReferenceError
}

const user = { name: "A" };
user.name = "B";  // ঠিক আছে
user = {};        // TypeError
```

❓ **ফলো-আপ:** "const দিয়ে object freeze করা যায়?" → জি, `Object.freeze(obj)` দিয়ে করা যায়, তবে সেটা shallow freeze, ভেতরের nested object বদলানো যাবে।

🔮 **আজ ও ভবিষ্যতে:** প্রফেশনাল টিমে ESLint-এর `no-var` ও `prefer-const` রুল চালু থাকে। const-first অভ্যাসটাই এখন স্ট্যান্ডার্ড।

---

## 2️⃣ Hoisting কী?

> 🎤 **বলুন:** Hoisting মানে JavaScript কোড চালানোর আগে একটা creation phase-এ scope-এর সব declaration মেমরিতে রেজিস্টার করে রাখে। দেখে মনে হয় declaration গুলো উপরে উঠে গেছে। মূল নিয়ম হলো, শুধু declaration hoist হয়, initialization হয় না।

📖 **বিস্তারিত ব্যাখ্যা**

| ধরন | Hoisting আচরণ |
|---|---|
| `var` | Hoist হয়, প্রাথমিক মান `undefined` |
| `let` / `const` | Hoist হয়, কিন্তু initialize হয় না (TDZ) |
| Function declaration | সম্পূর্ণ function সহ hoist |
| Function expression / arrow | ভেরিয়েবলের নিয়ম অনুযায়ী |
| Class | Hoist হয়, কিন্তু TDZ-তে থাকে |

💻 **কোড**

```javascript
console.log(x); // undefined
var x = 5;

sayHi();        // "Hi!" কাজ করে
function sayHi() { console.log("Hi!"); }

greet();        // TypeError: greet is not a function
var greet = function () { console.log("Hello"); };
```

শেষ উদাহরণে `greet` hoist হয়ে `undefined` হয়েছে, তাই call করলে `undefined()` চালানোর চেষ্টা হয়।

❓ **ফলো-আপ:** "Hoisting কি কোড আক্ষরিকভাবে উপরে সরিয়ে দেয়?" → না। Engine আগে scope স্ক্যান করে declaration গুলো মেমরিতে বরাদ্দ করে, কোড যেখানে ছিল সেখানেই থাকে।

🔮 **আজ ও ভবিষ্যতে:** ES Modules ও const-first স্টাইলে hoisting-নির্ভর কোড লেখার দরকার পড়ে না। আগে declare, তারপর ব্যবহার, এটাই পরিষ্কার কোডের নিয়ম।

---

## 3️⃣ Primitive data type গুলো কী কী?

> 🎤 **বলুন:** JavaScript-এ সাতটা primitive type আছে: string, number, bigint, boolean, undefined, null আর symbol। এগুলো immutable এবং value হিসেবে কপি হয়। বাকি সবকিছু object, যেগুলো reference হিসেবে কপি হয়।

📖 **বিস্তারিত ব্যাখ্যা**

| Type | উদাহরণ | মন্তব্য |
|---|---|---|
| `string` | `"hello"` | Immutable |
| `number` | `42`, `3.14`, `NaN`, `Infinity` | IEEE 754 floating point |
| `bigint` | `12345678901234567890n` | বড় পূর্ণসংখ্যার জন্য |
| `boolean` | `true` / `false` | |
| `undefined` | | মান assign হয়নি |
| `null` | | ইচ্ছাকৃত খালি |
| `symbol` | `Symbol("id")` | ইউনিক identifier |

Primitive-এ `"abc".length` লিখলে JavaScript সাময়িকভাবে wrapper object তৈরি করে, কিন্তু primitive নিজে object নয়।

💻 **কোড**

```javascript
let a = 10;
let b = a;
b = 20;
console.log(a); // 10, কারণ কপি হয়েছে

const o1 = { n: 1 };
const o2 = o1;   // reference কপি
o2.n = 99;
console.log(o1.n); // 99
```

❓ **ফলো-আপ:** "`0.1 + 0.2 === 0.3` কেন false?" → Number IEEE 754 floating point ব্যবহার করে, তাই দশমিকে সামান্য ভুল থাকে। টাকার হিসাবে পয়সায় integer বা BigInt ব্যবহার করা ভালো।

🔮 **আজ ও ভবিষ্যতে:** TypeScript-এ type নিশ্চিত করা এখন সাধারণ অনুশীলন, তবে primitive আর reference-এর পার্থক্য বোঝা না থাকলে state mutation-এর বাগ এড়ানো যায় না।

---

## 4️⃣ == আর === এর পার্থক্য কী?

> 🎤 **বলুন:** `==` loose equality, দুই দিকের type আলাদা হলে আগে type coercion করে তারপর তুলনা করে। `===` strict equality, type ও value দুটোই মিলতে হয়, কোনো coercion হয় না। তাই আমি সবসময় `===` ব্যবহার করি।

📖 **বিস্তারিত ব্যাখ্যা**

একমাত্র গ্রহণযোগ্য ব্যতিক্রম: `value == null` দিয়ে একসাথে `null` ও `undefined` চেক করা। Object তুলনায় দুটোই reference দেখে, তাই `{} === {}` সবসময় false। `NaN` নিজের সমানও নয়, তাই `Number.isNaN()` বা `Object.is()` ব্যবহার করতে হয়।

💻 **কোড**

```javascript
5 == "5"            // true
5 === "5"           // false
0 == false          // true
0 === false         // false
null == undefined   // true
null === undefined  // false
NaN === NaN         // false
{} === {}           // false (আলাদা reference)
```

❓ **ফলো-আপ:** "NaN কীভাবে চেক করবেন?" → `Number.isNaN(value)`, কারণ `NaN === NaN` false।

🔮 **আজ ও ভবিষ্যতে:** ESLint-এর `eqeqeq` রুল আর TypeScript এখন প্রায় সব প্রজেক্টে ডিফল্ট, তাই `===` ই শেষ কথা।

---

## 5️⃣ Closure কীভাবে কাজ করে? উদাহরণ দিন।

> 🎤 **বলুন:** Closure হলো এমন function, যে তার নিজের lexical scope-এর variable মনে রাখে, এমনকি বাইরের function শেষ হয়ে গেলেও। JavaScript-এ function তৈরির সময় সে তার চারপাশের scope-এর reference সাথে নিয়ে নেয়, সেটাই closure। নিচের counter উদাহরণে `count` বাইরে থেকে পাওয়া যায় না, কিন্তু ভেতরের function প্রতিবার সেটা বাড়ায়।

📖 **বিস্তারিত ব্যাখ্যা**

**বাস্তব ব্যবহার:**
1. Data privacy, মানে private state তৈরি
2. Function factory, কনফিগ সহ function বানানো
3. Callback ও event handler-এ বাইরের state ধরে রাখা
4. Memoization, debounce ও throttle
5. React Hooks (`useState`, `useEffect`)

**সতর্কতা:** অপ্রয়োজনীয় বড় object ধরে রাখলে memory leak হতে পারে। কাজ শেষে reference `null` করুন বা event listener সরিয়ে দিন।

💻 **কোড**

```javascript
function createCounter() {
  let count = 0;            // private variable
  return function () {
    count++;
    return count;
  };
}
const counter = createCounter();
counter(); // 1
counter(); // 2

// ক্লাসিক লুপ সমস্যা
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i), 100); // 3, 3, 3
for (let j = 0; j < 3; j++) setTimeout(() => console.log(j), 100); // 0, 1, 2
```

❓ **ফলো-আপ:** "var-এর লুপে 3, 3, 3 কেন আসে?" → সব callback একই `i` ভাগ করে, আর লুপ শেষে `i` তখন 3। `let` প্রতি iteration-এ নতুন binding দেয়।

🔮 **আজ ও ভবিষ্যতে:** React-এ stale closure বোঝা মানে hooks-এর সবচেয়ে সাধারণ বাগ নিজেই ধরতে পারা। এটি ভবিষ্যতেও React ও অন্য ফ্রেমওয়ার্কে সমান প্রাসঙ্গিক থাকবে।

---

## 6️⃣ null আর undefined-এর পার্থক্য কী?

> 🎤 **বলুন:** undefined মানে variable declare হয়েছে কিন্তু মান দেওয়া হয়নি, এটা engine নিজে বসায়। আর null মানে আমি ইচ্ছে করে বলছি যে এখানে কোনো মান নেই। একটা পুরনো বাগ হলো `typeof null` দেয় "object"।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | `undefined` | `null` |
|---|---|---|
| কে বসায় | JavaScript engine | ডেভেলপার |
| অর্থ | মান দেওয়া হয়নি | ইচ্ছাকৃতভাবে খালি |
| `typeof` | `"undefined"` | `"object"` (বাগ) |
| `Number(x)` | `NaN` | `0` |
| JSON-এ | বাদ পড়ে যায় | `null` থাকে |

💻 **কোড**

```javascript
let a;                           // undefined
function f() {}
console.log(f());                // undefined (return নেই)
const obj = {};
console.log(obj.missing);        // undefined

let b = null;                    // ইচ্ছাকৃত খালি
const name = user?.profile?.name ?? "Guest";
```

❓ **ফলো-আপ:** "`??` আর `||` এর পার্থক্য?" → `||` সব falsy মানে (`0`, `""` সহ) ডিফল্টে চলে যায়, আর `??` শুধু `null` ও `undefined`-এ যায়।

🔮 **আজ ও ভবিষ্যতে:** Prisma ও API response-এ optional ফিল্ড সাধারণত `null` আসে, আর `?.` ও `??` এখন আধুনিক JavaScript-এর স্বাভাবিক অংশ।

---

## 7️⃣ Arrow function কী এবং সাধারণ function থেকে কীভাবে আলাদা?

> 🎤 **বলুন:** Arrow function হলো ES6-এর সংক্ষিপ্ত সিনট্যাক্স। সবচেয়ে বড় পার্থক্য, এর নিজের `this` নেই, বাইরের scope-এর `this` ব্যবহার করে, যাকে lexical this বলে। এতে `arguments` নেই, `new` দিয়ে constructor হয় না। তাই callback-এ arrow ভালো, কিন্তু object method বা constructor-এ নয়।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | Regular function | Arrow function |
|---|---|---|
| `this` | কলের ধরন অনুযায়ী নিজস্ব | বাইরের scope থেকে (lexical) |
| `arguments` | আছে | নেই (`...args` ব্যবহার করুন) |
| `new` দিয়ে constructor | হয় | হয় না |
| `prototype` | আছে | নেই |
| Hoisting | declaration হলে হয় | হয় না |

**কখন arrow:** callback, `map`/`filter`/`reduce`, Promise chain। **কখন নয়:** object method, constructor।

💻 **কোড**

```javascript
const add = (a, b) => a + b;
const getUser = () => ({ id: 1 });   // object return করতে ()

const person = {
  name: "Alamin",
  regular() {
    setTimeout(function () { console.log(this.name); }, 100); // undefined
  },
  arrow() {
    setTimeout(() => { console.log(this.name); }, 100);       // "Alamin"
  },
};
```

❓ **ফলো-আপ:** "Arrow function কি অবজেক্টের মেথড হিসেবে ব্যবহার করা যায়?" → সাধারণত না, কারণ সেখানে নিজস্ব `this` দরকার হয়।

🔮 **আজ ও ভবিষ্যতে:** React ও Node.js-এর আধুনিক কোডে arrow function-ই callback-এর প্রচলিত স্টাইল।

---

## 8️⃣ Scope chain কী?

> 🎤 **বলুন:** কোনো variable খুঁজতে JavaScript প্রথমে বর্তমান scope দেখে, না পেলে এক ধাপ বাইরে যায়, এভাবে global পর্যন্ত যায়। এই শিকলটাই scope chain। এটা lexical scoping-এর উপর ভিত্তি করে, অর্থাৎ function কোথায় লেখা হয়েছে সেটাই ঠিক করে সে কোন scope দেখতে পাবে, কোথায় call হয়েছে সেটা নয়।

📖 **বিস্তারিত ব্যাখ্যা**

- Scope-এর ধরন: Global, Function, Block (`let`/`const`), Module
- কোথাও না পেলে `ReferenceError`
- **Shadowing:** ভেতরের scope-এ একই নামের variable থাকলে সেটা বাইরেরটিকে আড়াল করে

💻 **কোড**

```javascript
const global = "global";

function outer() {
  const outerVar = "outer";

  function inner() {
    const innerVar = "inner";
    console.log(innerVar);  // নিজের scope
    console.log(outerVar);  // এক ধাপ বাইরে
    console.log(global);    // global
    console.log(missing);   // ReferenceError
  }
  inner();
}

let x = 1;
function f() {
  let x = 2;     // বাইরের x-কে shadow করছে
  console.log(x); // 2
}
```

❓ **ফলো-আপ:** "Lexical scope আর dynamic scope-এর পার্থক্য?" → JavaScript lexical, অর্থাৎ লেখার জায়গা ঠিক করে scope, call করার জায়গা নয়।

🔮 **আজ ও ভবিষ্যতে:** Scope chain-ই closure আর module system বোঝার ভিত্তি, তাই এটি বুঝলে বাকি অনেক ধারণা সহজ হয়।

---

## 9️⃣ Temporal Dead Zone (TDZ) কী?

> 🎤 **বলুন:** `let`, `const` ও `class` hoist হয়, কিন্তু declaration লাইনে পৌঁছানোর আগ পর্যন্ত initialize হয় না। scope-এর শুরু থেকে ওই লাইন পর্যন্ত সময়টাকেই TDZ বলে। এর মধ্যে variable ধরলে `ReferenceError` আসে। এটা আসলে `var`-এর নীরব `undefined` বাগ থেকে বাঁচানোর জন্য।

📖 **বিস্তারিত ব্যাখ্যা**

TDZ-এর সুবিধা হলো ভুল করলে সাথে সাথে error পাওয়া যায়, নীরবে `undefined` নিয়ে বাগ লুকিয়ে থাকে না। এমনকি `typeof` ও TDZ-তে থাকা variable-এ error দেয়, যদিও declare-ই-না-হওয়া variable-এ `"undefined"` দেয়।

💻 **কোড**

```javascript
{
  // TDZ শুরু
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 10;     // TDZ শেষ
  console.log(a); // 10
}

typeof undeclared; // "undefined" (declare-ই হয়নি)
{
  typeof tdzVar;   // ReferenceError (TDZ!)
  let tdzVar;
}
```

❓ **ফলো-আপ:** "TDZ আছে বলে কি let hoist হয় না?" → হয়, কিন্তু initialize হয় না। এটাই TDZ-এর আসল কারণ।

🔮 **আজ ও ভবিষ্যতে:** এই কারণেই আধুনিক JavaScript-এ `let` ও `const`-কে `var`-এর নিরাপদ বিকল্প ধরা হয়।

---

## 🔟 Pure function কী? উদাহরণ দিন।

> 🎤 **বলুন:** Pure function হলো যেটা একই input দিলে সবসময় একই output দেয়, আর বাইরের কোনো কিছু বদলায় না, মানে কোনো side effect নেই। এতে test করা, debug করা আর cache করা অনেক সহজ। বাস্তবে পুরো অ্যাপ pure হয় না, তাই আমি business logic pure রাখি আর API বা DB-র কাজ প্রান্তে সীমাবদ্ধ রাখি।

📖 **বিস্তারিত ব্যাখ্যা**

**দুটি শর্ত:** ১) একই input-এ একই output, ২) কোনো side effect নেই (বাইরের state, DOM, ফাইল, নেটওয়ার্ক, ডাটাবেস বদলায় না, input mutate করে না)।

**সুবিধা:** সহজ test, সহজ debug, memoize করা যায়, concurrency-তে নিরাপদ, React/Redux reducer-এর ভিত্তি।

💻 **কোড**

```javascript
// Pure
const add = (a, b) => a + b;
const addItem = (cart, item) => [...cart, item]; // নতুন array

// Impure
let total = 0;
function addToTotal(n) { total += n; return total; } // বাইরের state বদলায়
function getRandom() { return Math.random(); }       // ফলাফল বদলায়
function mutate(arr) { arr.push(1); return arr; }    // input mutate
```

❓ **ফলো-আপ:** "API call কি pure?" → না, নেটওয়ার্ক একটি side effect। তাই side effect আলাদা স্তরে রেখে ভেতরের logic pure রাখা হয়।

🔮 **আজ ও ভবিষ্যতে:** React reducer ও functional স্টাইল pure function-এর উপরেই দাঁড়িয়ে, আর বড় প্রজেক্টে এটাই maintainability বাড়ায়।

---

## 1️⃣1️⃣ Function declaration আর function expression-এর পার্থক্য কী?

> 🎤 **বলুন:** Declaration সম্পূর্ণ hoist হয়, তাই ডিফাইন করার আগেও call করা যায়। Expression-এ শুধু variable hoist হয়, মান হয় না, তাই আগে call করলে error আসে। Expression anonymous হতে পারে, আর callback বা IIFE-তে বেশি ব্যবহার হয়।

📖 **বিস্তারিত ব্যাখ্যা**

| বিষয় | Declaration | Expression |
|---|---|---|
| Hoisting | সম্পূর্ণ function সহ | শুধু variable (মান নয়) |
| ডিক্লেয়ারের আগে call | করা যায় | করা যায় না |
| নাম | বাধ্যতামূলক | ঐচ্ছিক |
| ব্যবহার | সাধারণ utility function | callback, IIFE, মান হিসেবে পাস করা |

💻 **কোড**

```javascript
// Declaration
function greet(name) { return `Hello, ${name}`; }

// Expression
const greet2 = function (name) { return `Hello, ${name}`; };

// Named function expression (debug-এ সুবিধা)
const greet3 = function greetFn(name) { /* ... */ };

hello();                              // কাজ করে
function hello() { console.log("hi"); }

bye();                                // error
const bye = function () { console.log("bye"); };
```

❓ **ফলো-আপ:** "Arrow function কোন ধরনের?" → Function expression-এর একটি রূপ।

🔮 **আজ ও ভবিষ্যতে:** টিমে ESLint/Prettier দিয়ে একটি ধারাবাহিক স্টাইল ঠিক করে নেওয়াই এখন স্বাভাবিক অনুশীলন।

---

## 1️⃣2️⃣ Default parameter কী?

> 🎤 **বলুন:** Function-এ argument না দিলে বা `undefined` দিলে যে ডিফল্ট মান ব্যবহার হয়, সেটাই default parameter। মনে রাখার বিষয়, শুধু `undefined`-এই এটা কাজ করে, `null` বা `0`-তে করে না। Destructuring-এর সাথে মিলিয়ে config object-এও খুব কাজে লাগে।

📖 **বিস্তারিত ব্যাখ্যা**

- Default মান প্রতিবার runtime-এ মূল্যায়িত হয়, তাই expression বা function call-ও দেওয়া যায়
- আগের parameter পরের default-এ ব্যবহার করা যায়
- `null`, `0`, `""`, `false`-এ default কাজ করে না

💻 **কোড**

```javascript
function greet(name = "Guest", greeting = "Hello") {
  return `${greeting}, ${name}!`;
}
greet();                  // "Hello, Guest!"
greet(undefined, "Hi");   // "Hi, Guest!"
greet(null);              // "Hello, null!"

function createUser(name, role = "CLIENT", id = generateId()) { /* ... */ }

function connect({ host = "localhost", port = 5432 } = {}) {
  console.log(host, port);
}
connect();                // localhost 5432
connect({ port: 3000 });  // localhost 3000
```

❓ **ফলো-আপ:** "`greet(null)` এ default কেন কাজ করে না?" → কারণ default শুধু `undefined`-এ চালু হয়, `null` একটি বৈধ মান।

🔮 **আজ ও ভবিষ্যতে:** আধুনিক SDK ও লাইব্রেরির API-তে config object ও default parameter-এর প্যাটার্ন সর্বত্র দেখা যায়।

---

## 1️⃣3️⃣ typeof অপারেটর কী এবং এর return মান কী কী?

> 🎤 **বলুন:** typeof কোনো মানের ধরন string আকারে বলে দেয়। এর আটটি সম্ভাব্য মান: string, number, bigint, boolean, undefined, symbol, function ও object। কিছু ফাঁদ আছে: `typeof null` দেয় object, array-ও দেয় object, তাই array চেক করতে `Array.isArray` ব্যবহার করি।

📖 **বিস্তারিত ব্যাখ্যা**

| মান | `typeof` ফলাফল |
|---|---|
| `"hi"` | `"string"` |
| `42`, `NaN` | `"number"` |
| `10n` | `"bigint"` |
| `true` | `"boolean"` |
| `undefined` | `"undefined"` |
| `Symbol()` | `"symbol"` |
| `function(){}` | `"function"` |
| `{}`, `[]`, `null`, `new Date()` | `"object"` |

💻 **কোড**

```javascript
typeof null;            // "object" (ঐতিহাসিক বাগ)
typeof [];              // "object"
typeof NaN;             // "number"
typeof undeclaredVar;   // "undefined" (error দেয় না)

Array.isArray([]);                          // true
value === null;                             // null চেক
Object.prototype.toString.call(new Date()); // "[object Date]"
```

❓ **ফলো-আপ:** "Array কীভাবে চেক করবেন?" → `Array.isArray(value)`।

🔮 **আজ ও ভবিষ্যতে:** TypeScript আর Zod-এর মতো টুলে type validation এখন প্রায় বাধ্যতামূলক, কিন্তু `typeof`-ই তার মূল ভিত্তি।

---

## 1️⃣4️⃣ Type coercion কী? উদাহরণসহ বলুন।

> 🎤 **বলুন:** এক ধরনের মানকে অন্য ধরনে রূপান্তর করাই type coercion। JavaScript নিজে করলে implicit, আর আমি `Number()` বা `String()` দিয়ে করলে explicit। যেমন `+` এর সাথে string থাকলে string হয়, কিন্তু `-` এ number। তাই ফর্মের ডেটা হিসাব করার আগে আমি explicit রূপান্তর করে নিই।

📖 **বিস্তারিত ব্যাখ্যা**

**Falsy মান মাত্র ৮টি:** `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`। বাকি সব truthy, এমনকি `"0"`, `[]`, `{}`-ও।

**ফাঁদ এড়ানোর উপায়:** `===` ব্যবহার, explicit রূপান্তর, আর `||` এর জায়গায় `??` (কারণ `0` বা `""` বৈধ মান হতে পারে)।

💻 **কোড**

```javascript
// Implicit
"5" + 1;        // "51"
"5" - 1;        // 4
"5" * "2";      // 10
true + 1;       // 2
[] + [];        // ""
null + 1;       // 1
undefined + 1;  // NaN

// Explicit
Number("42");      // 42
Number("abc");     // NaN
String(123);       // "123"
Boolean("");       // false
parseInt("10px");  // 10

const qty = input || 10;   // input 0 হলে 10 হয়ে যায় (ভুল!)
const qty2 = input ?? 10;  // শুধু null/undefined হলে 10
```

❓ **ফলো-আপ:** "`[] == false` কেন true?" → দুই দিকই number-এ রূপান্তরিত হয়ে `0 == 0` হয়ে যায়। এই জন্যই `===` ব্যবহার করা উচিত।

🔮 **আজ ও ভবিষ্যতে:** ফর্ম বা query string-এর সব মান string হয়ে আসে, তাই প্রোডাকশনে explicit রূপান্তর ও validation ছাড়া হিসাব করা ঝুঁকিপূর্ণ।

---

## 1️⃣5️⃣ IIFE কী?

> 🎤 **বলুন:** IIFE মানে Immediately Invoked Function Expression, অর্থাৎ যে function ডিফাইন হওয়ার সাথে সাথেই চলে। বন্ধনী দিয়ে মোড়ানো হয় যাতে এটা expression হিসেবে ধরা হয়। আগে global scope দূষণ এড়াতে খুব ব্যবহার হতো, এখন ES Modules ও `let`/`const` আসায় কম লাগে, তবে async কোড চালানো আর legacy কোডে এখনও দেখা যায়।

📖 **বিস্তারিত ব্যাখ্যা**

**কেন ব্যবহার হয়:**
1. Private scope তৈরি, global namespace দূষণ এড়ানো
2. Module pattern, closure দিয়ে private ডেটা
3. এক-বারের ইনিশিয়ালাইজেশন
4. Async কোড চালানো (top-level await-এর আগে)

💻 **কোড**

```javascript
(function () {
  const secret = "hidden";
  console.log("চলছে!");
})();

(() => { console.log("Arrow IIFE"); })();

(async () => {
  const res = await fetch("/api/data");
  console.log(await res.json());
})();

const Counter = (function () {
  let count = 0;
  return { inc: () => ++count, get: () => count };
})();
Counter.inc();
Counter.get(); // 1
```

❓ **ফলো-আপ:** "বন্ধনী ছাড়া লিখলে কী হয়?" → JavaScript সেটাকে function declaration ধরে নেয়, আর নাম না থাকলে SyntaxError দেয়।

🔮 **আজ ও ভবিষ্যতে:** নতুন প্রজেক্টে ES Modules ব্যবহার হয়, কিন্তু পুরনো লাইব্রেরি ও bundled কোড পড়তে IIFE বোঝা জরুরি।

---

## ✅ ইন্টারভিউয়ের আগে শেষ মুহূর্তের চেকলিস্ট

- [ ] `var`, `let`, `const` এবং scope-এর পার্থক্য মুখস্থ নয়, বুঝে বলতে পারি
- [ ] Hoisting আর TDZ একসাথে ব্যাখ্যা করতে পারি
- [ ] Closure-এর একটি নিজের বানানো উদাহরণ বলতে পারি
- [ ] `==` বনাম `===` এবং falsy মানের তালিকা জানি
- [ ] Arrow function-এর `this` আচরণ বুঝিয়ে বলতে পারি