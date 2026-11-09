# JavaScript Fundamentals I — জব ইন্টারভিউ সংক্ষিপ্ত উত্তর (বাংলায়)

**কীভাবে ব্যবহার করবেন:** প্রতিটি উত্তর ৩–৪ লাইনে, মুখে বলার মতো করে লেখা। শেষে তিনটি অংশ: মূল উত্তর, ছোট কোড, আর **AI যুগের এক লাইন** (ইন্টারভিউয়ারকে বলার জন্য ভিন্ন মাত্রা যোগ করতে)।

---

## Q1. var vs let vs const

**উত্তর:** `var` function-scoped, hoisted (মান `undefined`), re-declare ও re-assign করা যায়। `let` block-scoped, re-assign করা যায় না। `const` block-scoped, re-assign হয় না, তবে object/array-এর ভেতরের মান বদলানো যায়। ডিফল্টে `const`, লাগলে `let`, `var` এড়িয়ে চলা।

```javascript
const user = { name: "A" };
user.name = "B";  // OK
user = {};        // TypeError
```

**AI যুগ:** AI কখনো পুরনো স্টাইলে `var` লেখে; তাই `no-var` / `prefer-const` ESLint রুল রাখা উচিত।

---

## Q2. Hoisting

**উত্তর:** Engine কোড চালানোর আগে scope-এর declaration গুলো মেমরিতে রেজিস্টার করে। শুধু **declaration** hoist হয়, **initialization** নয়। `var` → `undefined`; `let`/`const` → TDZ; function declaration → সম্পূর্ণ hoist।

```javascript
console.log(x); // undefined
var x = 5;
```

**AI যুগ:** Hoisting জানলে AI-লেখা অদ্ভুত ক্রমের কোড নিরাপদে refactor করা যায়।

---

## Q3. Primitive data types

**উত্তর:** ৭টি: `string`, `number`, `bigint`, `boolean`, `undefined`, `null`, `symbol`। এগুলো **immutable** ও **pass by value**। বাকি সব (array, function, object) **reference type**।

**AI যুগ:** AI API-র JSON-এ `null`/`undefined`/string-number গুলিয়ে যায়; type জানলে Zod validation ঠিকভাবে লেখা যায়।

---

## Q4. == vs ===

**উত্তর:** `==` আগে type coercion করে তারপর তুলনা করে (`5 == "5"` → true)। `===` type ও value দুটোই মিলায়, coercion করে না (`5 === "5"` → false)। সবসময় `===` ব্যবহার করি। একমাত্র ব্যতিক্রম `x == null`।

**AI যুগ:** `eqeqeq` রুল চালু রাখলে নীরব coercion বাগ AI বা মানুষ কারো কোডেই ঢুকতে পারে না।

---

## Q5. Closure

**উত্তর:** Function যখন তার নিজের lexical scope-এর variable মনে রাখে, বাইরের function শেষ হয়ে গেলেও, তখন সেটাকে closure বলে। ব্যবহার: private data, function factory, callback, debounce, React hooks।

```javascript
function createCounter() {
  let count = 0;
  return () => ++count;
}
const c = createCounter();
c(); // 1
c(); // 2
```

সতর্কতা: অপ্রয়োজনীয় বড় ডেটা ধরে রাখলে memory leak।

**AI যুগ:** React-এ AI-কোডের সবচেয়ে সাধারণ বাগ **stale closure**; closure বুঝলে এটা দ্রুত ধরা যায়।

---

## Q6. null vs undefined

**উত্তর:** `undefined` মানে declare হয়েছে কিন্তু মান দেওয়া হয়নি (engine বসায়)। `null` মানে ডেভেলপার ইচ্ছাকৃতভাবে "খালি" বলছে। `typeof null === "object"` (পুরনো বাগ)। `null == undefined` true, `null === undefined` false। `?.` ও `??` দিয়ে দুটোকেই সামলানো যায়।

**AI যুগ:** DB (Prisma) ও LLM response-এ optional ফিল্ড `null` হয়ে আসে, JSON-এ `undefined` বাদ পড়ে যায়।

---

## Q7. Arrow function vs regular function

**উত্তর:** Arrow function (ES6) সংক্ষিপ্ত সিনট্যাক্স। পার্থক্য: ১) নিজস্ব `this` নেই, বাইরের scope থেকে নেয় (lexical this); ২) `arguments` নেই; ৩) `new` দিয়ে constructor হয় না; ৪) `prototype` নেই। Callback-এ ভালো, object method/constructor-এ নয়।

```javascript
const add = (a, b) => a + b;
const getUser = () => ({ id: 1 });
```

**AI যুগ:** AI সবজায়গায় arrow বসায়, ভুল জায়গায় বসালে `this` ভেঙে যায়, রিভিউয়ে ধরতে হবে।

---

## Q8. Scope chain

**উত্তর:** ভেরিয়েবল খুঁজতে JS প্রথমে নিজের scope, না পেলে এক ধাপ বাইরে, এভাবে global পর্যন্ত যায়। এই শিকলের নাম scope chain। এটি **lexical** — function কোথায় লেখা হয়েছে সেটাই দেখানো কেন scope দেখা যাবে। না পেলে `ReferenceError`। ভেতরের নাম বাইরেরটিকে আড়াল করলে সেটা shadowing।

**AI যুগ:** `"use strict"` ও ES modules AI-লেখা accidental global ও shadowing বাগ ধরিয়ে দেয়।

---

## Q9. Temporal Dead Zone

**উত্তর:** `let`/`const`/`class` hoist হয় কিন্তু declaration লাইনে পৌঁছানোর আগ পর্যন্ত initialize হয় না। scope-এর শুরু থেকে সেই লাইন পর্যন্ত সময়টাই TDZ; এর ভেতর অ্যাক্সেস করলে `ReferenceError`। উদ্দেশ্য: `var`-এর নীরব `undefined` বাগ এড়ানো।

```javascript
console.log(a); // ReferenceError
let a = 10;
```

**AI যুগ:** AI কখনো `const` function ব্যবহারের নিচে রাখে, ফলে TDZ error আসে; ক্রম ঠিক করতে হয়।

---

## Q10. Pure function

**উত্তর:** দুই শর্ত: ১) একই input-এ সবসময় একই output; ২) কোনো side effect নেই (বাইরের state বদলায় না, input mutate করে না)। সুবিধা: টেস্ট, ডিবাগ ও memoize করা সহজ।

```javascript
const addItem = (cart, item) => [...cart, item]; // pure
let total = 0;
const addToTotal = n => (total += n);              // impure
```

**AI যুগ:** Pure function-এ AI দিয়ে unit test লেখানো সবচেয়ে সহজ ও নির্ভরযোগ্য।

---

## Q11. Function declaration vs function expression

**উত্তর:** Declaration (`function f(){}`) সম্পূর্ণ hoist হয়, তাই ডিক্লেয়ারের আগেও call করা যায়। Expression (`const f = function(){}`) শুধু variable hoist হয়, মান নয়, তাই আগে call করলে error। Expression anonymous হতে পারে, callback ও IIFE-তে ব্যবহৃত হয়। Arrow function ও expression-এর আরেক রূপ।

**AI যুগ:** প্রজেক্টে একটি ধারাবাহিক স্টাইল (ESLint/Prettier) থাকলে AI-ও সেই কনভেনশন মেনে লেখে।

---

## Q12. Default parameters

**উত্তর:** Argument দেওয়া না হলে বা `undefined` হলে ব্যবহৃত হওয়া ডিফল্ট মান। `null`, `0`, `""`-এ ডিফল্ট কাজ করে না। Runtime-এ মূল্যায়িত হয়, আগের প্র্যামিটার ব্যবহার করা যায়, destructuring-এর সাথে বেশ কাজের।

```javascript
function greet(name = "Guest") { return `Hi, ${name}`; }
greet();      // Hi, Guest
greet(null);  // Hi, null
```

**AI যুগ:** SDK কনফিগ `{ model, temperature = 0.7 } = {}` এভাবে পরিষ্কার API ডিজাইন করে।

---

## Q13. typeof অপারেটর

**উত্তর:** মানের ধরন string আকারে দেয়। ৮টি return মান: `"string"`, `"number"`, `"bigint"`, `"boolean"`, `"undefined"`, `"symbol"`, `"function"`, `"object"`। ফাঁদ: `typeof null` → `"object"`, `typeof []` → `"object"` (তাই `Array.isArray`), `typeof NaN` → `"number"`, declare-না-হওয়া ভেরিয়েবলে error দেয় না।

**AI যুগ:** LLM-এর আউটপুট অবিশ্বস্ত ধরে type validation (Zod/TypeScript) বাধ্যতামূলক করুন।

---

## Q14. Type coercion

**উত্তর:** এক টাইপের মান অন্য টাইপে রূপান্তর। **Implicit** (JS নিজে করে) ও **explicit** (`Number()`, `String()`, `Boolean()`)। `+` এ string প্রাধান্য পায়, `-`/`*` এ number। Falsy মাত্র ৮টি: `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`; বাকি সব truthy (`[]`, `{}`, `"0"` ও)।

```javascript
"5" + 1;   // "51"
"5" - 1;   // 4
true + 1;  // 2
input ?? 10 // 0 বৈধ মান হলে || এর জায়গায় ??
```

**AI যুগ:** ফর্ম/query string-এর সবকিছু string; AI-কোড সেটা number ধরে হিসাব করলে বিলিং/ডেটা বাগ হয়।

---

## Q15. IIFE

**উত্তর:** Function যা ডিফাইন হওয়ার সাথে সাথেই চলে। বন্ধনী দিয়ে মোড়ানো হয় যাতে expression হিসেবে ধরা হয়। ব্যবহার: private scope, global দূষণ এড়ানো, module pattern, একবারের ইনিশিয়ালাইজেশন, async কোড চালানো। ES modules ও `let`/`const` আসায় প্রয়োজন কমেছে, তবে legacy ও bundled কোডে এখনও পাওয়া যায়।

```javascript
(function () {
  const secret = "hidden";
})();

(async () => {
  const res = await fetch("/api/data");
})();
```

**AI যুগ:** AI-কোডে `(async () => {...})()` প্যাটার্ন প্রায়ই আসে, তাই বুঝতে পারা জরুরি।

---

## শেষ মুহূর্তের ৩টি কথা (ইন্টারভিউয়ে বলার জন্য)

1. "AI কোড লেখে, কিন্তু সেটা যাচাই, debug ও দায়িত্ব নেওয়ার জন্য মূল বিষয়গুলো জানা জরুরি।"
2. "আমি শুধু মুখস্থ করি না; কেন এমন হয় আর কখন কোনটা ব্যবহার করব, সেটা বুঝি।"
3. "Tool বদলাবে, কিন্তু JavaScript-এর এই মৌলিক নিয়মগুলো TypeScript, React, Node.js-এ একই থাকবে।"
