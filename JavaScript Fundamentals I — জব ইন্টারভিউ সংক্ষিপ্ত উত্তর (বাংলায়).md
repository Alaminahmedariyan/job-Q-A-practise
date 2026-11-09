# 🟣 JavaScript Fundamentals I — ইন্টারভিউ সংক্ষিপ্ত উত্তর

**টপিক:** Variables, Data Types, Functions & Scope

> প্রতিটি প্রশ্নে তিনটি অংশ আছে: 🎤 **মুখে যেভাবে বলবেন**, 📌 **মূল পয়েন্ট**, 🔮 **আজকের দিনে ও ভবিষ্যতে**। ইন্টারভিউতে প্রথম অংশটি প্রায় হুবহু বলতে পারবেন।

---

## 1️⃣ var, let ও const-এর পার্থক্য কী?

> 🎤 **বলুন:** জি, তিনটাই variable declare করার উপায়। পার্থক্য scope আর reassign-এ। var function-scoped, আর let ও const block-scoped। const-এ আবার মান assign করা যায় না, তবে object-এর ভেতরের মান বদলানো যায়। আমি সবসময় const দিয়ে শুরু করি, দরকার হলে let ব্যবহার করি, আর var এড়িয়ে চলি।

📌 **মূল পয়েন্ট**
- `var`: function scope, hoisted (মান `undefined`), redeclare চলে
- `let`: block scope, reassign চলে, redeclare চলে না
- `const`: block scope, reassign চলে না (object mutate চলে)

```javascript
const user = { name: "A" };
user.name = "B";  // ঠিক আছে
user = {};        // TypeError
```

🔮 **আজ ও ভবিষ্যতে:** প্রফেশনাল টিমে ESLint-এর `no-var` ও `prefer-const` রুল থাকে, তাই const-first অভ্যাসটাই স্ট্যান্ডার্ড।

---

## 2️⃣ Hoisting কী?

> 🎤 **বলুন:** Hoisting মানে JavaScript কোড চালানোর আগে scope-এর declaration গুলো মেমরিতে তুলে রাখে। শুধু declaration যায়, মান বসানো যায় না। তাই var-এ undefined পাই, আর let ও const-এ error আসে।

📌 **মূল পয়েন্ট**
- `var` → মান `undefined`
- `let` / `const` / `class` → TDZ-তে থাকে
- Function declaration → পুরো function সহ hoist
- Function expression → ভেরিয়েবলের নিয়মে চলে

```javascript
console.log(x); // undefined
var x = 5;

sayHi();        // কাজ করে
function sayHi() { console.log("Hi"); }
```

🔮 **আজ ও ভবিষ্যতে:** ES Modules ও const-first স্টাইলে hoisting-নির্ভর কোড লেখার দরকার পড়ে না। আগে declare, তারপর ব্যবহার।

---

## 3️⃣ Primitive data type গুলো কী কী?

> 🎤 **বলুন:** JavaScript-এ সাতটা primitive: string, number, bigint, boolean, undefined, null আর symbol। এগুলো immutable এবং value হিসেবে কপি হয়। বাকি সবকিছু object, যেগুলো reference হিসেবে কপি হয়।

📌 **মূল পয়েন্ট**
- ৭টি primitive: `string`, `number`, `bigint`, `boolean`, `undefined`, `null`, `symbol`
- Primitive: pass by value
- Object, Array, Function: pass by reference

```javascript
let a = 10; let b = a; b = 20;   // a এখনও 10
const o1 = { n: 1 }; const o2 = o1;
o2.n = 99;                       // o1.n-ও 99
```

🔮 **আজ ও ভবিষ্যতে:** টাকার হিসাবে `0.1 + 0.2` সমস্যা এড়াতে পয়সায় integer বা BigInt ব্যবহার করা প্রোডাকশনের ভালো অভ্যাস।

---

## 4️⃣ == আর === এর পার্থক্য কী?

> 🎤 **বলুন:** == আগে type coercion করে তারপর তুলনা করে, আর === type ও value দুটোই মেলায়, কোনো coercion করে না। তাই আমি সবসময় === ব্যবহার করি। একমাত্র ব্যতিক্রম, `x == null` দিয়ে null আর undefined একসাথে চেক করা।

📌 **মূল পয়েন্ট**
- `==` → loose equality (coercion হয়)
- `===` → strict equality (type ও value মিলতে হবে)
- Object তুলনা হয় reference ধরে

```javascript
5 == "5"    // true
5 === "5"   // false
{} === {}   // false (আলাদা reference)
```

🔮 **আজ ও ভবিষ্যতে:** ESLint-এর `eqeqeq` রুল আর TypeScript এখন প্রায় সব প্রজেক্টে ডিফল্ট, তাই `===` ই শেষ কথা।

---

## 5️⃣ Closure কীভাবে কাজ করে? উদাহরণ দিন।

> 🎤 **বলুন:** Closure হলো এমন function, যে তার নিজের lexical scope-এর variable মনে রাখে, এমনকি বাইরের function শেষ হয়ে গেলেও। নিচের counter উদাহরণে count বাইরে থেকে পাওয়া যায় না, কিন্তু ভেতরের function সেটা মনে রেখে প্রতিবার বাড়ায়।

📌 **মূল পয়েন্ট**
- ব্যবহার: private data, function factory, callback, debounce
- React Hooks আসলে closure-এর উপরেই দাঁড়িয়ে
- সতর্কতা: অপ্রয়োজনীয় বড় ডেটা ধরে রাখলে memory leak হতে পারে

```javascript
function createCounter() {
  let count = 0;
  return () => ++count;
}
const c = createCounter();
c(); // 1
c(); // 2
```

🔮 **আজ ও ভবিষ্যতে:** React-এ stale closure বোঝা মানে hooks-এর সবচেয়ে সাধারণ বাগ নিজেই ধরতে পারা।

---

## 6️⃣ null আর undefined-এর পার্থক্য কী?

> 🎤 **বলুন:** undefined মানে variable declare হয়েছে কিন্তু মান দেওয়া হয়নি, এটা engine নিজে বসায়। আর null মানে আমি ইচ্ছে করে বলছি যে এখানে কোনো মান নেই। একটা পুরনো বাগ হলো `typeof null` দেয় "object"।

📌 **মূল পয়েন্ট**
- `undefined`: মান দেওয়া হয়নি (সিস্টেম বসায়)
- `null`: ইচ্ছাকৃতভাবে খালি (ডেভেলপার বসায়)
- `null == undefined` true, `null === undefined` false

```javascript
let a;                 // undefined
let b = null;          // ইচ্ছাকৃত খালি
const name = user?.profile?.name ?? "Guest";
```

🔮 **আজ ও ভবিষ্যতে:** আধুনিক কোডে `?.` ও `??` দিয়ে দুটোকেই সহজে সামলানো হয়। Prisma ও API response-এও optional ফিল্ড সাধারণত `null` আসে।

---

## 7️⃣ Arrow function কী এবং সাধারণ function থেকে কীভাবে আলাদা?

> 🎤 **বলুন:** Arrow function হলো ES6-এর সংক্ষিপ্ত সিনট্যাক্স। সবচেয়ে বড় পার্থক্য, এর নিজের this নেই, বাইরের scope-এর this ব্যবহার করে। এতে arguments নেই, এবং new দিয়ে constructor হিসেবে ব্যবহার করা যায় না। তাই callback-এ arrow ভালো, কিন্তু object method বা constructor-এ নয়।

📌 **মূল পয়েন্ট**
- Lexical `this` (বাইরের scope থেকে নেয়)
- `arguments` নেই, `prototype` নেই
- `new` দিয়ে constructor হয় না

```javascript
const add = (a, b) => a + b;
const getUser = () => ({ id: 1 });
```

🔮 **আজ ও ভবিষ্যতে:** React ও Node.js-এর আধুনিক কোডে callback আর `map`/`filter`/`reduce`-এ arrow function-ই প্রচলিত স্টাইল।

---

## 8️⃣ Scope chain কী?

> 🎤 **বলুন:** কোনো variable খুঁজতে JavaScript প্রথমে বর্তমান scope দেখে, না পেলে এক ধাপ বাইরে যায়, এভাবে global পর্যন্ত যায়। এই ধাপে ধাপে খোঁজার শিকলই scope chain। এটা lexical, অর্থাৎ function কোথায় লেখা হয়েছে সেটাই ঠিক করে সে কোন scope দেখতে পাবে।

📌 **মূল পয়েন্ট**
- Local → বাইরের function → global, এই ক্রমে খোঁজে
- কোথাও না পেলে `ReferenceError`
- ভেতরের একই নামের variable বাইরেরটাকে shadow করে

```javascript
const g = "global";
function outer() {
  const o = "outer";
  function inner() {
    console.log(o, g); // দুটোই পায়
  }
  inner();
}
```

🔮 **আজ ও ভবিষ্যতে:** Scope chain-ই closure আর module system বোঝার ভিত্তি।

---

## 9️⃣ Temporal Dead Zone (TDZ) কী?

> 🎤 **বলুন:** let, const ও class hoist হয়, কিন্তু declaration লাইনে পৌঁছানোর আগ পর্যন্ত initialize হয় না। scope-এর শুরু থেকে ওই লাইন পর্যন্ত সময়টাকেই TDZ বলে। এর মধ্যে variable ধরলে ReferenceError আসে। এটা আসলে var-এর নীরব undefined বাগ থেকে বাঁচানোর জন্য।

📌 **মূল পয়েন্ট**
- TDZ = scope-এর শুরু থেকে declaration লাইন পর্যন্ত
- ভেতরে অ্যাক্সেস করলে `ReferenceError`
- বাগ তাড়াতাড়ি ধরা পড়ে, এটাই সুবিধা

```javascript
console.log(a); // ReferenceError
let a = 10;
```

🔮 **আজ ও ভবিষ্যতে:** এই কারণেই আধুনিক JavaScript-এ `let` ও `const`-কে `var`-এর নিরাপদ বিকল্প ধরা হয়।

---

## 🔟 Pure function কী? উদাহরণ দিন।

> 🎤 **বলুন:** Pure function হলো যেটা একই input দিলে সবসময় একই output দেয়, আর বাইরের কোনো কিছু বদলায় না। এতে test করা, debug করা আর cache করা অনেক সহজ। বাস্তবে পুরো অ্যাপ pure হয় না, তাই আমি business logic pure রাখি আর API বা DB-র কাজ প্রান্তে সীমাবদ্ধ রাখি।

📌 **মূল পয়েন্ট**
- একই input → একই output
- কোনো side effect নেই, input mutate করে না
- সুবিধা: সহজ test, debug ও memoization

```javascript
const addItem = (cart, item) => [...cart, item]; // pure

let total = 0;
const addToTotal = n => (total += n);            // impure
```

🔮 **আজ ও ভবিষ্যতে:** React reducer ও functional স্টাইল pure function-এর উপরেই দাঁড়িয়ে, আর বড় প্রজেক্টে এটাই maintainability বাড়ায়।

---

## 1️⃣1️⃣ Function declaration আর function expression-এর পার্থক্য কী?

> 🎤 **বলুন:** Declaration সম্পূর্ণ hoist হয়, তাই ডিফাইন করার আগেও call করা যায়। Expression-এ শুধু variable hoist হয়, মান হয় না, তাই আগে call করলে error আসে। Expression anonymous হতে পারে, আর callback বা IIFE-তে বেশি ব্যবহার হয়।

📌 **মূল পয়েন্ট**
- Declaration: পুরো function hoist হয়
- Expression: শুধু variable hoist, মান নয়
- Arrow function-ও এক ধরনের expression

```javascript
hello();                       // কাজ করে
function hello() {}

bye();                         // error
const bye = function () {};
```

🔮 **আজ ও ভবিষ্যতে:** টিমে ESLint/Prettier দিয়ে একটি ধারাবাহিক স্টাইল ঠিক করে নেওয়াই এখন স্বাভাবিক অনুশীলন।

---

## 1️⃣2️⃣ Default parameter কী?

> 🎤 **বলুন:** Function-এ argument না দিলে বা undefined দিলে যে ডিফল্ট মান ব্যবহার হয়, সেটাই default parameter। মনে রাখার বিষয়, শুধু undefined-এই এটা কাজ করে, null বা 0-তে করে না। destructuring-এর সাথে মিলিয়ে config object-এও খুব কাজে লাগে।

📌 **মূল পয়েন্ট**
- শুধু `undefined` হলে default ব্যবহার হয়
- আগের parameter পরেরটার default-এ ব্যবহার করা যায়
- destructuring-এর সাথে config object-এ বহুল ব্যবহৃত

```javascript
function greet(name = "Guest") {
  return "Hi, " + name;
}
greet();       // Hi, Guest
greet(null);   // Hi, null
```

🔮 **আজ ও ভবিষ্যতে:** আধুনিক SDK ও লাইব্রেরির API-তে `{ port = 3000 } = {}` ধরনের কনফিগ প্যাটার্ন সর্বত্র দেখা যায়।

---

## 1️⃣3️⃣ typeof অপারেটর কী এবং এর return মান কী কী?

> 🎤 **বলুন:** typeof কোনো মানের ধরন string আকারে বলে দেয়। এর আটটি সম্ভাব্য মান: string, number, bigint, boolean, undefined, symbol, function ও object। কিছু ফাঁদ আছে: `typeof null` দেয় object, array-ও দেয় object, তাই array চেক করতে `Array.isArray` ব্যবহার করি।

📌 **মূল পয়েন্ট**
- ৮টি মান: `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol`, `function`, `object`
- `typeof null` → `"object"` (ঐতিহাসিক বাগ)
- `typeof NaN` → `"number"`

```javascript
typeof null;        // "object"
typeof [];          // "object"
Array.isArray([]);  // true
typeof undeclared;  // "undefined" (error নয়)
```

🔮 **আজ ও ভবিষ্যতে:** TypeScript আর Zod-এর মতো টুলে type validation এখন প্রায় বাধ্যতামূলক, কিন্তু typeof-ই তার মূল ভিত্তি।

---

## 1️⃣4️⃣ Type coercion কী? উদাহরণসহ বলুন।

> 🎤 **বলুন:** এক ধরনের মানকে অন্য ধরনে রূপান্তর করাই type coercion। JavaScript নিজে করলে implicit, আর আমি `Number()` বা `String()` দিয়ে করলে explicit। যেমন + এর সাথে string থাকলে string হয়, কিন্তু - এ number। তাই ফর্মের ডেটা হিসাব করার আগে আমি explicit রূপান্তর করে নিই।

📌 **মূল পয়েন্ট**
- Falsy মাত্র ৮টি: `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`
- বাকি সব truthy (যেমন `[]` ও `{}`)
- `0` বৈধ মান হলে `||` এর বদলে `??` ব্যবহার করি

```javascript
"5" + 1    // "51"
"5" - 1    // 4
true + 1   // 2
const qty = input ?? 10;  // 0 হলেও ঠিক থাকে
```

🔮 **আজ ও ভবিষ্যতে:** ফর্ম বা query string-এর সব মান string হয়ে আসে, তাই প্রোডাকশনে explicit রূপান্তর ও validation ছাড়া হিসাব করা ঝুঁকিপূর্ণ।

---

## 1️⃣5️⃣ IIFE কী?

> 🎤 **বলুন:** IIFE মানে Immediately Invoked Function Expression, অর্থাৎ যে function ডিফাইন হওয়ার সাথে সাথেই চলে। বন্ধনী দিয়ে মোড়ানো হয় যাতে এটা expression হিসেবে ধরা হয়। আগে global scope দূষণ এড়াতে খুব ব্যবহার হতো, এখন ES Modules ও let/const আসায় কম লাগে, তবে async কোড চালানো আর legacy কোডে এখনও দেখা যায়।

📌 **মূল পয়েন্ট**
- ডিফাইন হওয়ামাত্র চলে
- private scope ও module pattern তৈরিতে ব্যবহার
- async IIFE: top-level await না থাকলে কাজে লাগে

```javascript
(function () {
  const secret = "hidden";
})();

(async () => {
  const res = await fetch("/api/data");
})();
```

🔮 **আজ ও ভবিষ্যতে:** নতুন প্রজেক্টে ES Modules ব্যবহার হয়, কিন্তু পুরনো লাইব্রেরি ও bundled কোড পড়তে IIFE বোঝা জরুরি।