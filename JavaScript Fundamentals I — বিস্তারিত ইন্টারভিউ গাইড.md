# JavaScript Fundamentals I — বিস্তারিত ইন্টারভিউ গাইড

**টপিক:** Variables, Data Types, Functions & Scope **ভাষা:** বাংলা (কোড ও টেকনিক্যাল টার্ম ইংরেজিতে) **লক্ষ্য:** জব ইন্টারভিউয়ের জন্য গভীর বোঝাপড়া + AI যুগে কোন জিনিসটা কেন জরুরি, সেই দৃষ্টিভঙ্গি

> **AI যুগের মূল কথা:** আজকাল Copilot, Claude বা ChatGPT দিয়ে কোড লেখা সহজ। কিন্তু AI-এর লেখা কোড **review, debug ও ব্যাখ্যা** করতে পারাটাই ডেভেলপারের আসল মূল্য। ইন্টারভিউয়ে তাই "কীভাবে কাজ করে" আর "কেন এমন হয়" জানাটা সবচেয়ে বেশি যাচাই করা হয়। এই ১৫টি প্রশ্ন সেই ভিত্তিই তৈরি করে।

---

## Q1. var, let এবং const-এর পার্থক্য কী?

তিনটিই variable declare করার কীওয়ার্ড, কিন্তু scope, hoisting আর reassign-এর নিয়মে তফাত আছে।

| বৈশিষ্ট্য | var | let | const |
| --- | --- | --- | --- |
| Scope | Function scope | Block scope | Block scope |
| Hoisting | হয়, মান `undefined` | হয়, কিন্তু TDZ-তে থাকে | হয়, কিন্তু TDZ-তে থাকে |
| Re-declare | করা যায় | করা যায় না | করা যায় না |
| Re-assign | করা যায় | করা যায় | করা যায় না |
| Initialize বাধ্যতামূলক? | না | না | হ্যাঁ |
| Global-এ `window` property হয়? | হ্যাঁ | না | না |

```javascript
function demo() {
  if (true) {
    var a = 1;   // function scope
    let b = 2;   // block scope
    const c = 3; // block scope
  }
  console.log(a); // 1
  console.log(b); // ReferenceError
  console.log(c); // ReferenceError
}
```

**গুরুত্বপূর্ণ বিষয়:** `const` মানে value **immutable** নয়, binding **reassign করা যায় না**। Object বা array-র ভেতরের মান বদলানো যায়।

```javascript
const user = { name: "Alamin" };
user.name = "Islam";   // ঠিক আছে
user = {};             // TypeError: Assignment to constant variable
```

**Best practice:** ডিফল্টভাবে `const` ব্যবহার করুন, reassign লাগলে `let`, আর `var` এড়িয়ে চলুন।

**AI যুগের দৃষ্টিকোণ:** AI কখনো কখনো পুরনো স্টাইলে `var` দিয়ে কোড লেখে। Review-এর সময় এটা ধরতে পারা এবং `const`/`let`-এ বদলানো আপনার কাজ। ESLint-এর `no-var` ও `prefer-const` রুল চালু রাখলে AI-জেনারেটেড কোডও স্বয়ংক্রিয়ভাবে ঠিক থাকে।

---

## Q2. Hoisting কী?

JavaScript কোড চালানোর আগে একটি **creation phase** থাকে, যেখানে engine scope-এর ভেতরের সব declaration মেমরিতে রেজিস্টার করে। দেখে মনে হয় declaration গুলো scope-এর **উপরে উঠে গেছে**। এটাই hoisting।

**মূল নিয়ম:** শুধু **declaration** hoist হয়, **initialization** নয়।

```javascript
console.log(x); // undefined (error নয়)
var x = 5;

sayHi();        // "Hi!" কাজ করে
function sayHi() { console.log("Hi!"); }

console.log(y); // ReferenceError
let y = 10;
```

| ধরন | Hoisting আচরণ |
| --- | --- |
| `var` | Hoist হয়, প্রাথমিক মান `undefined` |
| `let` / `const` | Hoist হয়, কিন্তু initialize হয় না (TDZ) |
| Function declaration | সম্পূর্ণ function সহ hoist হয় |
| Function expression / arrow | variable-এর নিয়ম অনুযায়ী (`var` হলে `undefined`, `let`/`const` হলে TDZ) |
| Class | Hoist হয়, কিন্তু TDZ-তে থাকে |

```javascript
greet(); // TypeError: greet is not a function
var greet = function () { console.log("Hello"); };
```

এখানে `greet` hoist হয়ে `undefined` হয়েছে, তাই call করলে `undefined()` চালানোর চেষ্টা হয়।

**ইন্টারভিউ টিপ:** "কোড আক্ষরিকভাবে উপরে সরে যায়" বলবেন না। সঠিক ব্যাখ্যা হলো: engine আগে scope স্ক্যান করে declaration গুলো মেমরিতে বরাদ্দ করে।

**AI যুগের দৃষ্টিকোণ:** AI-জেনারেটেড কোডে function ব্যবহারের পরে define করা থাকলে সেটা hoisting-এর কারণে কাজ করে, কিন্তু readability খারাপ হয়। Hoisting বুঝলে এমন কোড নিরাপদে refactor করা যায়।

---

## Q3. JavaScript-এর Primitive data type গুলো কী কী?

JavaScript-এ **৭টি primitive type** আছে:

1. **string**: `"hello"`
2. **number**: `42`, `3.14`, `NaN`, `Infinity`
3. **bigint**: `12345678901234567890n` (বড় পূর্ণসংখ্যার জন্য)
4. **boolean**: `true` / `false`
5. **undefined**: মান assign করা হয়নি
6. **null**: ইচ্ছাকৃতভাবে "কোনো মান নেই"
7. **symbol**: ইউনিক identifier, `Symbol("id")`

**Primitive-এর বৈশিষ্ট্য:**

- **Immutable**: মান সরাসরি বদলানো যায় না
- **Pass by value**: কপি হয়ে যায়
- Object নয়, কিন্তু property access করলে সাময়িকভাবে wrapper object তৈরি হয় (`"abc".length`)

```javascript
let a = 10;
let b = a;
b = 20;
console.log(a); // 10, কারণ কপি হয়েছে

const obj1 = { n: 1 };
const obj2 = obj1;   // reference কপি
obj2.n = 99;
console.log(obj1.n); // 99
```

বাকি সব কিছু (array, function, date ইত্যাদি) **Object (reference type)**।

**প্রো টিপ:** `0.1 + 0.2 !== 0.3` হয় কারণ number IEEE 754 floating point। টাকা-পয়সার হিসাবে integer (পয়সায়) বা `BigInt`/লাইব্রেরি ব্যবহার করুন।

**AI যুগের দৃষ্টিকোণ:** AI API থেকে আসা JSON ডেটায় প্রায়ই `null` বনাম `undefined` বা string বনাম number গুলিয়ে যায়। Type জানা থাকলে validation (যেমন Zod) ঠিকভাবে লেখা যায়।

---

## Q4. == এবং === এর পার্থক্য কী?

- `==` (loose equality): দুই দিকের type আলাদা হলে আগে **type coercion** করে, তারপর তুলনা করে
- `===` (strict equality): type ও value **দুটোই** মিলতে হবে, কোনো coercion হয় না

```javascript
5 == "5"          // true
5 === "5"         // false
0 == false        // true
0 === false       // false
null == undefined // true
null === undefined// false
NaN == NaN        // false
NaN === NaN       // false (Number.isNaN বা Object.is ব্যবহার করুন)
```

**কখন কোনটি:** সবসময় `===` ব্যবহার করুন। একমাত্র গ্রহণযোগ্য ব্যতিক্রম: `value == null` দিয়ে একসাথে `null` ও `undefined` চেক করা।

**Object তুলনা:** দুটোই reference তুলনা করে।

```javascript
{} === {}         // false (আলাদা reference)
[1] == [1]        // false
```

**AI যুগের দৃষ্টিকোণ:** `==`-এর কারণে হওয়া বাগ নীরবে ঘটে এবং ডিবাগ করা কঠিন। ESLint-এ `eqeqeq` রুল রাখলে AI বা মানুষ, যে-ই কোড লিখুক, সমস্যা ধরা পড়ে।

---

## Q5. Closure কীভাবে কাজ করে? উদাহরণ সহ ব্যাখ্যা করুন।

**Closure** হলো এমন একটি function, যা তার **নিজের lexical scope-এর variable গুলো মনে রাখে**, এমনকি বাইরের function-এর execution শেষ হয়ে গেলেও।

JavaScript-এ function তৈরির সময় সে তার চারপাশের scope-এর reference সাথে নিয়ে নেয়। এটাই closure।

```javascript
function createCounter() {
  let count = 0;            // private variable
  return function () {
    count++;
    return count;
  };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
// বাইরে থেকে count সরাসরি পাওয়া যায় না
```

`createCounter()` শেষ হয়ে গেছে, তবু ভেতরের function `count` মনে রেখেছে।

**বাস্তব ব্যবহার:**

1. **Data privacy / encapsulation**: private state তৈরি
2. **Function factory**: কনফিগারেশন সহ function বানানো
3. **Callback ও event handler**: বাইরের state ধরে রাখা
4. **Memoization, debounce, throttle**
5. **React Hooks**: `useState`, `useEffect` ভেতরে closure-এর উপর নির্ভর করে

```javascript
function multiplier(factor) {
  return (n) => n * factor;
}
const double = multiplier(2);
console.log(double(5)); // 10
```

**ক্লাসিক লুপ সমস্যা:**

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// 3, 3, 3 (সব closure একই i ভাগ করে)

for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 100);
}
// 0, 1, 2 (let প্রতি iteration-এ নতুন binding দেয়)
```

**সতর্কতা:** Closure অপ্রয়োজনীয় বড় object ধরে রাখলে **memory leak** হতে পারে। কাজ শেষে reference `null` করুন বা event listener সরিয়ে দিন।

**AI যুগের দৃষ্টিকোণ:** React-এ AI-জেনারেটেড কোডে সবচেয়ে সাধারণ বাগগুলোর একটি হলো **stale closure**, অর্থাৎ `useEffect` বা event handler পুরনো state ধরে রাখা। Closure ঠিকভাবে বুঝলে dependency array-র সমস্যা দ্রুত ধরা যায়।

---

## Q6. null এবং undefined-এর পার্থক্য কী?

- **undefined**: ভেরিয়েবল declare হয়েছে কিন্তু কোনো মান দেওয়া হয়নি। এটি JavaScript engine নিজে বসায়।
- **null**: ডেভেলপার ইচ্ছাকৃতভাবে বলছে "এখানে কোনো মান নেই"।

```javascript
let a;
console.log(a);              // undefined

function f() {}
console.log(f());            // undefined (return নেই)

const obj = {};
console.log(obj.missing);    // undefined

let b = null;                // ইচ্ছাকৃত খালি

console.log(typeof undefined); // "undefined"
console.log(typeof null);      // "object" (পুরনো বাগ, আজও আছে)
console.log(null == undefined);  // true
console.log(null === undefined); // false
console.log(Number(null));       // 0
console.log(Number(undefined));  // NaN
```

**কখন কোনটি:** "মান এখনো সেট হয়নি" বোঝাতে `undefined` (সিস্টেমের কাজ), আর "ইচ্ছে করে খালি" বোঝাতে `null` ব্যবহার করুন। আধুনিক কোডে `??` (nullish coalescing) এবং `?.` (optional chaining) দুটোকেই একসাথে সামলায়।

```javascript
const name = user?.profile?.name ?? "Guest";
```

**AI যুগের দৃষ্টিকোণ:** LLM API বা ডাটাবেস (Prisma) থেকে optional ফিল্ড `null` হিসেবে আসে, আর JSON-এ `undefined` থাকেই না (বাদ পড়ে যায়)। এই পার্থক্য না জানলে API response parse করতে গিয়ে বাগ হয়।

---

## Q7. Arrow function কী এবং সাধারণ function থেকে কীভাবে আলাদা?

Arrow function (ES6) হলো function লেখার সংক্ষিপ্ত সিনট্যাক্স।

```javascript
const add = (a, b) => a + b;          // implicit return
const square = n => n * n;            // এক প্যারামিটারে () ঐচ্ছিক
const getUser = () => ({ id: 1 });    // object return করতে () লাগে
```

**প্রধান পার্থক্য:**

| বিষয় | Regular function | Arrow function |
| --- | --- | --- |
| `this` | কলের ধরন অনুযায়ী নিজস্ব `this` | নিজের `this` নেই, **lexical this** (বাইরের scope থেকে) |
| `arguments` অবজেক্ট | আছে | নেই (rest `...args` ব্যবহার করুন) |
| `new` দিয়ে constructor | হয় | হয় না |
| `prototype` প্রপার্টি | আছে | নেই |
| Hoisting | declaration হলে হয় | হয় না (expression) |
| Method হিসেবে | উপযুক্ত | সাধারণত উপযুক্ত নয় |

```javascript
const person = {
  name: "Alamin",
  regular() {
    setTimeout(function () {
      console.log(this.name); // undefined (this হারিয়ে গেছে)
    }, 100);
  },
  arrow() {
    setTimeout(() => {
      console.log(this.name); // "Alamin" (বাইরের this)
    }, 100);
  },
};
```

**কখন arrow ব্যবহার করবেন:** callback, `map`/`filter`/`reduce`, Promise chain। **কখন নয়:** object method, constructor, যেখানে নিজস্ব `this` দরকার।

**AI যুগের দৃষ্টিকোণ:** AI প্রায় সব জায়গায় arrow function লেখে এবং কখনো কখনো class method বা Express handler-এ ভুল জায়গায় ব্যবহার করে `this` ভেঙে ফেলে। কোথায় lexical this লাগবে আর কোথায় লাগবে না, সেই বোধ রিভিউয়ে কাজে লাগে।

---

## Q8. Scope chain কী?

JavaScript যখন কোনো ভেরিয়েবল খোঁজে, তখন প্রথমে **বর্তমান scope**-এ দেখে। না পেলে **এক ধাপ বাইরের scope**-এ যায়, এভাবে **global scope** পর্যন্ত যায়। এই ধাপে ধাপে খোঁজার শিকলটাই scope chain। এটি **lexical scoping**-এর উপর ভিত্তি করে, অর্থাৎ function কোথায় **লেখা হয়েছে** সেটাই ঠিক করে সে কোন scope দেখতে পাবে (কোথায় call হয়েছে সেটা নয়)।

```javascript
const global = "global";

function outer() {
  const outerVar = "outer";

  function inner() {
    const innerVar = "inner";
    console.log(innerVar);  // নিজের scope
    console.log(outerVar);  // এক ধাপ বাইরে
    console.log(global);    // global
    console.log(missing);   // ReferenceError (শিকলে কোথাও নেই)
  }
  inner();
}
```

**Scope-এর ধরন:** Global, Function, Block (`let`/`const`), এবং Module scope।

**Shadowing:** ভেতরের scope-এ একই নামের ভেরিয়েবল থাকলে সেটি বাইরেরটিকে আড়াল করে।

```javascript
let x = 1;
function f() {
  let x = 2;     // বাইরের x-কে shadow করছে
  console.log(x); // 2
}
```

Scope chain-ই closure-এর ভিত্তি।

**AI যুগের দৃষ্টিকোণ:** AI-জেনারেটেড কোডে অসাবধানে shadowing বা accidental global (`let` ছাড়া assign) থাকতে পারে। `"use strict"` এবং ES modules এসব ধরিয়ে দেয়।

---

## Q9. Temporal Dead Zone (TDZ) কী?

`let`, `const` এবং `class` hoist হয়, কিন্তু **declaration লাইনে পৌঁছানোর আগ পর্যন্ত** initialize হয় না। scope-এর শুরু থেকে এই declaration লাইন পর্যন্ত সময়টাকে **Temporal Dead Zone** বলে। এই সময়ে ভেরিয়েবল অ্যাক্সেস করলে `ReferenceError` হয়।

```javascript
{
  // TDZ শুরু
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 10;     // TDZ শেষ
  console.log(a); // 10
}

console.log(typeof undeclared); // "undefined" (declare-ই হয়নি)
{
  console.log(typeof tdzVar);   // ReferenceError (TDZ!)
  let tdzVar;
}
```

**কেন TDZ আছে?** `var`-এর নীরব `undefined` বাগ এড়াতে। এখন ভুল হলে সাথে সাথে এরর পাওয়া যায়, যা ডিবাগে সুবিধা দেয়।

**AI যুগের দৃষ্টিকোণ:** কোড সাজানোর সময় AI অনেক সময় `const` ফাংশন ব্যবহারের নিচে রেখে দেয়, ফলে TDZ error আসে। এই এরর দেখলেই বোঝা যায় ডিক্লেয়ারেশনের ক্রম ঠিক করতে হবে।

---

## Q10. Pure function কী? একটি উদাহরণ দিন।

Pure function হলো এমন function যার দুটি শর্ত পূরণ হয়:

1. **একই input দিলে সবসময় একই output** দেয় (deterministic)
2. **কোনো side effect নেই**: বাইরের state, DOM, ফাইল, নেটওয়ার্ক বা ডাটাবেস বদলায় না, ইনপুটও mutate করে না

```javascript
// Pure
const add = (a, b) => a + b;

const addItem = (cart, item) => [...cart, item]; // নতুন array, পুরনোটা অক্ষত

// Impure
let total = 0;
function addToTotal(n) {
  total += n;           // বাইরের state বদলাচ্ছে
  return total;
}

function getRandom() { return Math.random(); }   // ফলাফল বদলায়
function mutate(arr) { arr.push(1); return arr; } // ইনপুট mutate
```

**সুবিধা:** টেস্ট করা সহজ, ডিবাগ সহজ, cache/memoize করা যায়, concurrency-তে নিরাপদ, React/Redux reducer-এর ভিত্তি।

**বাস্তবতা:** পুরো অ্যাপ pure হতে পারে না (API call, DB লাগেই)। কৌশল হলো **business logic pure রাখা** আর side effect একদম প্রান্তে (controller, service boundary) সীমাবদ্ধ রাখা।

**AI যুগের দৃষ্টিকোণ:** AI দিয়ে unit test লেখানো সবচেয়ে সহজ হয় pure function-এর ক্ষেত্রে, কারণ ইনপুট-আউটপুট স্পষ্ট। আপনার কোড যত pure, AI-সহায়তা তত নির্ভরযোগ্য এবং ভুল ধরাও তত সহজ।

---

## Q11. Function declaration এবং function expression-এর পার্থক্য কী?

```javascript
// Function Declaration
function greet(name) {
  return `Hello, ${name}`;
}

// Function Expression
const greet2 = function (name) {
  return `Hello, ${name}`;
};

// Named function expression (ডিবাগে সুবিধা)
const greet3 = function greetFn(name) { /* ... */ };
```

| বিষয় | Declaration | Expression |
| --- | --- | --- |
| Hoisting | সম্পূর্ণ function সহ hoist হয় | শুধু ভেরিয়েবল hoist হয় (মান নয়) |
| ডিক্লেয়ারের আগে call | করা যায় | করা যায় না |
| নাম | বাধ্যতামূলক | ঐচ্ছিক (anonymous হতে পারে) |
| ব্যবহার | সাধারণ utility function | callback, IIFE, মান হিসেবে পাস করা, conditional definition |

```javascript
hello();                    // কাজ করে
function hello() { console.log("hi"); }

bye();                      // TypeError/ReferenceError
const bye = function () { console.log("bye"); };
```

**টিপ:** Arrow function ও আসলে function expression-এর একটি রূপ। আধুনিক কোডে অনেক টিম `const fn = () => {}` পছন্দ করে কারণ এটি ডিক্লেয়ারেশনের আগে ব্যবহার ঠেকায়, আর কিছু টিম top-level function-এর জন্য declaration পছন্দ করে পড়ার সুবিধার জন্য। দুটোই গ্রহণযোগ্য, টিমের কনভেনশন মানুন।

**AI যুগের দৃষ্টিকোণ:** AI মিশ্র স্টাইলে কোড লিখতে পারে। প্রজেক্টে একটি ধারাবাহিক স্টাইল (ESLint/Prettier-এ বাঁধা) থাকলে AI-র আউটপুটও সেই কনভেনশনে আসে।

---

## Q12. Default parameter কী?

Function-এর প্যারামিটারে মান না দিলে বা `undefined` দিলে যে ডিফল্ট মান ব্যবহার হয় সেটাই default parameter (ES6)।

```javascript
function greet(name = "Guest", greeting = "Hello") {
  return `${greeting}, ${name}!`;
}

greet();                  // "Hello, Guest!"
greet("Alamin");          // "Hello, Alamin!"
greet(undefined, "Hi");   // "Hi, Guest!"
greet(null);              // "Hello, null!" (null-এ default কাজ করে না!)
```

**গুরুত্বপূর্ণ বিষয়:**

- শুধু `undefined`-এ default কাজ করে, `null`, `0`, `""`, `false`-এ নয়
- Default মান runtime-এ প্রতিবার মূল্যায়িত হয়, তাই এক্সপ্রেশন বা function call ও দেওয়া যায়
- আগের প্যারামিটার পরের default-এ ব্যবহার করা যায়
- Object destructuring-এর সাথে খুব ব্যবহৃত হয়

```javascript
function createUser(name, role = "CLIENT", id = generateId()) { /* ... */ }

function connect({ host = "localhost", port = 5432 } = {}) {
  console.log(host, port);
}
connect();               // localhost 5432
connect({ port: 3000 }); // localhost 3000
```

**AI যুগের দৃষ্টিকোণ:** AI-নির্ভর টুল বা SDK কনফিগ অবজেক্ট নেয় (`{ model, temperature = 0.7 }`)। Default parameter ও destructuring মিলিয়ে পরিষ্কার, নিরাপদ API ডিজাইন করা যায়।

---

## Q13. typeof অপারেটর কী এবং এর সম্ভাব্য return মান কী কী?

`typeof` একটি অপারেটর যা অপারেন্ডের ধরন **string** আকারে ফেরত দেয়।

| মান | typeof ফলাফল |
| --- | --- |
| `"hi"` | `"string"` |
| `42`, `NaN` | `"number"` |
| `10n` | `"bigint"` |
| `true` | `"boolean"` |
| `undefined` | `"undefined"` |
| `Symbol()` | `"symbol"` |
| `function(){}` | `"function"` |
| `{}`, `[]`, `null`, `new Date()` | `"object"` |

সম্ভাব্য return মান মোট **৮টি**: `"string"`, `"number"`, `"bigint"`, `"boolean"`, `"undefined"`, `"symbol"`, `"function"`, `"object"`।

**বিখ্যাত ফাঁদ:**

```javascript
typeof null;            // "object" (ঐতিহাসিক বাগ)
typeof [];              // "object" (Array.isArray ব্যবহার করুন)
typeof NaN;             // "number"
typeof undeclaredVar;   // "undefined" (error দেয় না)
```

**সঠিক চেক:**

```javascript
Array.isArray([]);                                      // true
value === null;                                         // null চেক
Object.prototype.toString.call(new Date());             // "[object Date]"
```

**AI যুগের দৃষ্টিকোণ:** LLM-এর ফেরত দেওয়া ডেটা অবিশ্বস্ত ধরে নিয়ে type validation (`typeof`, Zod, TypeScript) বাধ্যতামূলক করা উচিত।

---

## Q14. Type coercion কী? উদাহরণসহ বুঝিয়ে বলুন।

JavaScript-এ এক টাইপের মানকে অন্য টাইপে রূপান্তর করাকে type coercion বলে।

- **Implicit coercion**: JavaScript নিজে স্বয়ংক্রিয়ভাবে করে
- **Explicit coercion (type casting)**: ডেভেলপার নিজে করে (`Number()`, `String()`, `Boolean()`)

```javascript
// Implicit
"5" + 1;        // "51" (+ এ string প্রাধান্য পায়)
"5" - 1;        // 4   (- এ number)
"5" * "2";      // 10
true + 1;       // 2
[] + {};        // "[object Object]"
[] + [];        // ""
null + 1;       // 1
undefined + 1;  // NaN

// Explicit
Number("42");   // 42
Number("abc");  // NaN
String(123);    // "123"
Boolean("");    // false
parseInt("10px"); // 10
```

**Falsy মান (মাত্র ৮টি):** `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`। বাকি সব **truthy**, এমনকি `"0"`, `[]`, `{}` ও।

```javascript
if ([])  console.log("truthy");   // চলবে
if ("0") console.log("truthy");   // চলবে
```

**ফাঁদ এড়ানোর উপায়:** `===` ব্যবহার, explicit রূপান্তর, এবং `||`-এর জায়গায় `??` (কারণ `0` বা `""` বৈধ মান হতে পারে)।

```javascript
const qty = input || 10;   // input 0 হলে 10 হয়ে যায় (ভুল!)
const qty2 = input ?? 10;  // শুধু null/undefined হলে 10
```

**AI যুগের দৃষ্টিকোণ:** ফর্ম বা query string থেকে সব ডেটা string হিসেবে আসে, আর AI-জেনারেটেড কোড প্রায়ই সেটা number ধরে নিয়ে হিসাব করে ফেলে (`"5" + 1`)। প্রোডাকশন SaaS-এ এই ধরনের ভুল সরাসরি বিলিং বা ডেটা বাগ হয়ে দাঁড়ায়।

---

## Q15. IIFE (Immediately Invoked Function Expression) কী?

IIFE হলো এমন function যা **ডিফাইন হওয়ার সাথে সাথেই চলে**।

```javascript
(function () {
  const secret = "hidden";
  console.log("চলছে!");
})();

// Arrow IIFE
(() => {
  console.log("Arrow IIFE");
})();

// প্যারামিটার সহ
(function (name) {
  console.log(`Hello, ${name}`);
})("Alamin");

// Async IIFE (top-level await না থাকলে)
(async () => {
  const res = await fetch("/api/data");
  console.log(await res.json());
})();
```

বন্ধনী `()` দিয়ে মোড়ানো হয় যাতে JavaScript এটিকে declaration না ভেবে **expression** হিসেবে ধরে।

**কেন ব্যবহার হয়:**

1. **Private scope তৈরি**: global namespace দূষণ এড়ানো (`var` যুগে বহুল ব্যবহৃত)
2. **Module pattern**: closure দিয়ে private ডেটা
3. **এক-বারের ইনিশিয়ালাইজেশন**
4. **Async কোড চালানো** (top-level await-এর আগে)

```javascript
const Counter = (function () {
  let count = 0;
  return {
    inc: () => ++count,
    get: () => count,
  };
})();
Counter.inc();
console.log(Counter.get()); // 1
```

**বর্তমানে:** ES Modules ও block scope (`let`/`const`) আসায় IIFE-এর প্রয়োজন কমেছে, তবে Node scripts, bundler আউটপুট, ইন্টারভিউ এবং legacy কোডে এখনও দেখা যায়।

**AI যুগের দৃষ্টিকোণ:** পুরনো লাইব্রেরি, ব্রাউজার স্ক্রিপ্ট বা bundled কোড পড়তে গেলে IIFE সর্বত্র পাওয়া যায়। AI-র লেখা কোডে `(async () => {...})()` প্যাটার্নও প্রায়ই আসে, এর মানে বোঝা জরুরি।

---

## সারসংক্ষেপ: AI যুগে এই টপিকগুলো কেন গুরুত্বপূর্ণ

1. **Review দক্ষতা:** AI কোড লেখে, আপনি যাচাই করেন। `var`, `==`, stale closure, ভুল `this` চিনতে পারাটাই আপনার ভ্যালু।
2. **Debug দক্ষতা:** hoisting, TDZ, scope বোঝা থাকলে অদ্ভুত error দ্রুত ধরা যায়।
3. **Prompt করার দক্ষতা:** মৌলিক ধারণা জানা থাকলে AI-কে সঠিক ভাষায় নির্দেশ দেওয়া যায় (যেমন "closure ব্যবহার না করে pure function বানাও")।
4. **ইন্টারভিউয়ে পার্থক্য:** মুখস্থ উত্তরের বদলে "কেন" এবং "কখন" ব্যাখ্যা করতে পারলে আপনি AI-র চেয়ে আলাদা হয়ে দাঁড়ান।
5. **ভবিষ্যতের জন্য:** AI টুল বদলাবে, কিন্তু JavaScript-এর এই মৌলিক নিয়মগুলো TypeScript, React, Node.js সব জায়গায় একই থাকবে।
