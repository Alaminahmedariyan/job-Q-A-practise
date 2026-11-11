# 🟣 JavaScript Fundamentals II — Detailed Interview Guide (English)

**Topic:** Arrays, Objects, ES6+ & Async

> Every question has six parts:
> 🎤 **How to say it** · 📖 **Detailed explanation** · 🧠 **Simple analogy** · 💻 **Code** · ❓ **Follow-up question** · 🔮 **Today & the future**

---

## 1️⃣6️⃣ What is destructuring? Explain with array and object examples.

> 🎤 **Say:** Destructuring is a concise way to pull values out of an array or object into separate variables. With arrays it works by position, and with objects it works by property name. It also supports default values, renaming and nested extraction, which keeps code short and clean.

📖 **Detailed explanation**

| Aspect | Array destructuring | Object destructuring |
|---|---|---|
| Based on | Position | Property name |
| Brackets | `[ ]` | `{ }` |
| Skipping | Leave a gap: `[a, , c]` | Just pick the names you need |
| Renaming | Any variable name | `{ name: userName }` |
| Default value | `[a = 1]` | `{ age = 20 }` |
| Collect the rest | `[a, ...rest]` | `{ a, ...rest }` |

🧠 **Simple analogy:** Opening a parcel and placing each item on its own shelf. With an array the items are arranged in order, with an object each item has a label on it.

💻 **Code**

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

❓ **Follow-up:** "What happens if the value is `undefined`?" → The default value is used. But if the value is `null`, the default is **not** used.

🔮 **Today & future:** `const [state, setState] = useState()` and props destructuring are everyday React code. Mentioning it shows you are fluent in modern JavaScript.

---

## 1️⃣7️⃣ What are the spread and rest operators and how are they used?

> 🎤 **Say:** Both use `...` but they do opposite jobs. Spread expands an array or object into individual items, and rest collects many items into one array or object. I use spread to copy and merge, and rest to accept any number of function arguments. One thing to remember is that spread makes a shallow copy.

📖 **Detailed explanation**

| Aspect | Spread | Rest |
|---|---|---|
| Job | Expands | Collects |
| Where it appears | In calls, array/object literals | In parameters or destructuring |
| Used for | Copy, merge, pass arguments | Variable number of arguments |
| Rule | Can go anywhere | **Must be last** |

🧠 **Simple analogy:** Spread is turning a bag upside down and laying everything on the table. Rest is sweeping the leftover items on the table into a new bag.

💻 **Code**

```javascript
// Spread
const merged = [...[1, 2], ...[3, 4]];            // [1, 2, 3, 4]
const user2 = { ...user, role: "admin" };         // copy + new property
Math.max(...[5, 9, 2]);                           // 9

// Rest
const sum = (...nums) => nums.reduce((a, b) => a + b, 0);
sum(1, 2, 3);                                     // 6

const [head, ...tail] = [1, 2, 3];                // tail = [2, 3]
const { id, ...rest } = { id: 1, a: 2, b: 3 };    // rest = { a: 2, b: 3 }
```

⚠️ **Trap (shallow copy):**

```javascript
const a = { info: { x: 1 } };
const b = { ...a };
b.info.x = 99;
console.log(a.info.x); // 99, because the nested object is the same reference
```

❓ **Follow-up:** "What is the difference between a rest parameter and `arguments`?" → Rest is a real array, while `arguments` is an array-like object and does not exist in arrow functions.

🔮 **Today & future:** Spread is the most common pattern for updating React state immutably.

---

## 1️⃣8️⃣ What is the difference between map(), filter() and reduce()?

> 🎤 **Say:** All three are array methods that return a result without mutating the original array. `map` transforms each element and returns a new array of the same length. `filter` keeps only the elements that pass a test, giving a shorter array. `reduce` boils the entire array down to a single value, like a sum or an object.

📖 **Detailed explanation**

| Method | Job | Returns | Length |
|---|---|---|---|
| `map` | Transform every element | New array | Same |
| `filter` | Keep elements that pass a test | New array | Shorter or equal |
| `reduce` | Combine into one value | Any single value | n/a |

**Syntax of `reduce`:**

```javascript
array.reduce(callback(accumulator, currentValue, currentIndex, array), initialValue);
```

- `accumulator`: the result from the previous step (the `initialValue` on the first step)
- `currentValue`: the element being processed
- `currentIndex` (optional): the index of the current element
- `array` (optional): the array `reduce` was called on
- `initialValue` (optional): if omitted, the first element becomes the accumulator and iteration starts from the **second element**

⚠️ Calling `reduce` on an empty array without an `initialValue` throws a `TypeError`, so it is safest to always provide one.

🧠 **Simple analogy:** A factory line. `map` paints every product, `filter` removes the defective ones, and `reduce` packs everything into one box and gives the total.

💻 **Code**

```javascript
const nums = [1, 2, 3, 4, 5];

nums.map(n => n * 2);                  // [2, 4, 6, 8, 10]
nums.filter(n => n % 2 === 0);         // [2, 4]
nums.reduce((acc, n) => acc + n, 0);   // 15

// Chaining
const total = [
  { name: "A", price: 100, inStock: true },
  { name: "B", price: 50, inStock: false },
  { name: "C", price: 70, inStock: true },
]
  .filter(p => p.inStock)
  .map(p => p.price)
  .reduce((sum, price) => sum + price, 0);   // 170

// Counting with reduce
["a", "b", "a"].reduce((acc, ch) => {
  acc[ch] = (acc[ch] || 0) + 1;
  return acc;
}, {});                                       // { a: 2, b: 1 }
```

❓ **Follow-up:** "What is the difference between `forEach` and `map`?" → `forEach` returns nothing (`undefined`), while `map` returns a new array.

🔮 **Today & future:** Chaining these three is the foundation of modern data processing and React list rendering.

---

## 1️⃣9️⃣ What is the difference between for...in and for...of loops?

> 🎤 **Say:** `for...in` loops over an object's enumerable property **names (keys)**, including inherited ones. `for...of` loops over the **values** of an iterable such as an array, string, Map or Set. So for arrays I use `for...of`, and for objects I use `Object.entries()` with `for...of`.

📖 **Detailed explanation**

| Aspect | `for...in` | `for...of` |
|---|---|---|
| What you get | Keys (always strings) | Values |
| Works on | Objects (and arrays, though not recommended) | Iterables (Array, String, Map, Set) |
| Prototype chain | Included (inherited properties too) | Not applicable |
| On a plain object | Works | Does not work (`TypeError`) |

🧠 **Simple analogy:** `for...in` is reading the nameplates on each door, while `for...of` is looking at what is inside each room.

💻 **Code**

```javascript
const arr = ["a", "b"];
for (const i in arr) console.log(i);   // "0", "1" (string indexes)
for (const v of arr) console.log(v);   // "a", "b"

for (const ch of "Hi") console.log(ch); // "H", "i"

const obj = { x: 1, y: 2 };
for (const k in obj) console.log(k);                         // "x", "y"
for (const [k, v] of Object.entries(obj)) console.log(k, v);  // x 1, y 2
// for (const v of obj) {}  // TypeError: obj is not iterable
```

❓ **Follow-up:** "Why avoid `for...in` on arrays?" → Indexes come as strings, order is not guaranteed, and extra properties or enumerable properties from the prototype can show up.

🔮 **Today & future:** Modern code prefers `Object.entries()` with `for...of`, or array methods.

---

## 2️⃣0️⃣ What are template literals and tagged templates?

> 🎤 **Say:** Template literals are strings written with backticks that allow `${}` expressions and multi-line text directly. In a tagged template, a function receives the string pieces and the values separately, so you can process them however you like. styled-components and GraphQL's `gql` work exactly this way.

📖 **Detailed explanation**

- **Plain template literal:** backticks (`` ` ``), `${expression}`, multi-line support
- **Tagged template:** a function name followed directly by a template. The function receives an **array of strings** as the first argument and the **values** as the remaining arguments
- Uses: HTML/SQL escaping, styled-components, GraphQL, i18n

🧠 **Simple analogy:** A form letter has blanks where you fill in the name and date. A tagged template is like an assistant who checks or formats each value before filling the blanks.

💻 **Code**

```javascript
const name = "Alamin";

// Plain
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

❓ **Follow-up:** "What type is `strings` in a tagged template?" → An array of strings, which also has a `raw` property holding the unescaped original text.

🔮 **Today & future:** Tagged templates remain widely used in CSS-in-JS and GraphQL libraries.

---

## 2️⃣1️⃣ What is the event loop in JavaScript?

> 🎤 **Say:** JavaScript is single-threaded, meaning it does one thing at a time, yet it handles async work through the event loop. When the call stack is empty, the loop first drains the **microtask queue** (Promises), then takes one job from the **task queue** (setTimeout, events). That is why a Promise callback always runs before a `setTimeout` callback.

📖 **Detailed explanation**

| Part | Role |
|---|---|
| Call stack | Code that is running right now |
| Web APIs / Node APIs | Handle timers, network, DOM events (outside the JavaScript engine) |
| Microtask queue | Promise `.then`, `queueMicrotask`, **higher priority** |
| Task (macrotask) queue | `setTimeout`, `setInterval`, UI events |
| Event loop | Moves work from the queues onto the stack when it is empty |

**Order:** stack empty → **all microtasks** → **one** task → microtasks again → ...

🧠 **Simple analogy:** A single waiter (the stack). He hands orders to the kitchen (Web API) and serves other tables. When food is ready, VIP-line orders (microtasks) are served first, then the regular line (tasks) one at a time.

💻 **Code**

```javascript
console.log("1");                               // sync
setTimeout(() => console.log("2"), 0);          // task queue
Promise.resolve().then(() => console.log("3")); // microtask
console.log("4");                               // sync

// Output: 1, 4, 3, 2
```

❓ **Follow-up:** "Does `setTimeout(fn, 0)` run immediately?" → No. It goes to the task queue and only runs after the stack and all microtasks are done.

🔮 **Today & future:** Understanding the event loop is essential to avoid freezing the UI by splitting heavy work and to debug async bugs. Node.js uses the same idea with a few extra phases.

---

## 2️⃣2️⃣ Explain how Promises work.

> 🎤 **Say:** A Promise represents a result that will be available in the future. It has three states: pending, fulfilled and rejected. `.then()` handles success, `.catch()` handles failure and `.finally()` always runs. Promises can be chained to do work step by step, and `Promise.all` runs many in parallel.

📖 **Detailed explanation**

**States:** `pending` → `fulfilled` or `rejected`. Once settled, a Promise never changes again.

| Method | Behavior |
|---|---|
| `Promise.all([...])` | Array of results if all succeed, rejects if any one fails |
| `Promise.allSettled([...])` | Returns every outcome, success or failure |
| `Promise.race([...])` | The first one to settle (success or failure) |
| `Promise.any([...])` | The first **successful** one, errors only if all fail |

🧠 **Simple analogy:** Ordering at a restaurant and getting a token. While the food is being prepared the token is "pending". When the food arrives it is "fulfilled", and if the dish runs out it is "rejected".

💻 **Code**

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
  ok ? resolve("success") : reject(new Error("failed"));
});
```

❓ **Follow-up:** "What happens if an error is thrown inside `.then`?" → The next `.catch` in the chain handles it.

🔮 **Today & future:** Every modern API (fetch, Prisma, various SDKs) returns Promises.

---

## 2️⃣3️⃣ What is async/await and how does it improve upon Promises?

> 🎤 **Say:** async/await is syntax built on top of Promises so that async code reads top to bottom like synchronous code. An `async` function always returns a Promise, and `await` waits for a Promise to settle. Errors are handled with ordinary `try/catch`, which removes the clutter of `.then` chains.

📖 **Detailed explanation**

- An `async` function always returns a Promise
- `await` works only inside `async` functions (top-level `await` also works in ES modules)
- `await` does not block the whole program, it only pauses the rest of that function

**Common mistakes:**
1. Awaiting independent tasks one after another (slow), use `Promise.all` instead
2. Using `await` inside `forEach` (it does not wait), use `for...of` or `Promise.all(map(...))`
3. Forgetting `try/catch`

🧠 **Simple analogy:** A Promise chain is instructions torn into slips: "when this finishes, do that". async/await is the same instructions written straight down one page.

💻 **Code**

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

// Independent tasks in parallel
async function loadAll() {
  const [user, settings] = await Promise.all([getUser(), getSettings()]);
  return { user, settings };
}
```

❓ **Follow-up:** "What do you get if you call an async function without `await`?" → A Promise, not the value inside it.

🔮 **Today & future:** async/await is the standard in Node.js, Next.js and virtually all backend code.

---

## 2️⃣4️⃣ What is the difference between call(), apply() and bind()?

> 🎤 **Say:** All three let me set a function's `this` explicitly. `call` runs the function immediately with arguments passed one by one. `apply` does the same but takes the arguments as an array. `bind` does not run the function, it returns a new function with `this` locked in, which I can call later.

📖 **Detailed explanation**

| Method | When it runs | Arguments | Returns |
|---|---|---|---|
| `call(thisArg, a, b)` | Immediately | Individually | The function's result |
| `apply(thisArg, [a, b])` | Immediately | As an array | The function's result |
| `bind(thisArg, a)` | Later (new function) | Individually (partial) | A new function |

Memory trick: **A**pply = **A**rray, **C**all = **C**omma, **B**ind = **B**ound function.

🧠 **Simple analogy:** A phone (the function) and a SIM card (`this`). `call` means insert a SIM and make a call right now. `bind` means building a new phone with the SIM already inside, to use whenever you like.

💻 **Code**

```javascript
function intro(greeting, punct) {
  return `${greeting}, ${this.name}${punct}`;
}
const user = { name: "Alamin" };

intro.call(user, "Hello", "!");     // "Hello, Alamin!"
intro.apply(user, ["Hello", "!"]);  // "Hello, Alamin!"

const bound = intro.bind(user, "Hi");
bound("?");                         // "Hi, Alamin?"

// Classic use: keep `this` inside a callback
const counter = {
  n: 0,
  start() { setInterval(function () { this.n++; }.bind(this), 1000); },
};
```

❓ **Follow-up:** "Can `call` change `this` of an arrow function?" → No. An arrow function's `this` is lexical, so `call/apply/bind` cannot change it.

🔮 **Today & future:** Arrow functions reduced the need for `bind`, but it still shows up in classes and legacy code.

---

## 2️⃣5️⃣ What is prototypal inheritance in JavaScript?

> 🎤 **Say:** In JavaScript every object has a hidden link to another object called its prototype. If a property or method is not found, the engine follows that link upward, and that is the prototype chain. The `class` syntax is just sugar built on top of this, so prototypes still do the work underneath.

📖 **Detailed explanation**

- Every object has a `[[Prototype]]` (visible through `Object.getPrototypeOf(obj)`)
- Lookup order: the object itself → its prototype → that prototype's prototype → ... → `null`
- `__proto__` is the legacy accessor for an object's prototype, while `prototype` is a property of **functions** that becomes the prototype of objects created with `new`
- `hasOwnProperty()` / `Object.hasOwn()` tells you whether a property is the object's own

🧠 **Simple analogy:** Family inheritance. If you do not have something, ask your father; if he does not have it, ask your grandfather, and so on until the end of the line.

💻 **Code**

```javascript
const animal = { eat() { return "eating"; } };
const dog = Object.create(animal);   // dog's prototype = animal
dog.bark = () => "woof";

dog.bark();                          // its own
dog.eat();                           // from the prototype
Object.getPrototypeOf(dog) === animal; // true

// Constructor function
function Person(name) { this.name = name; }
Person.prototype.hello = function () { return "Hi " + this.name; };
new Person("A").hello();             // "Hi A"

// class (same thing, newer syntax)
class Student extends Person {
  study() { return this.name + " is studying"; }
}
```

❓ **Follow-up:** "What is the difference between `prototype` and `__proto__`?" → `prototype` is a property of functions, while `__proto__` is the link on every object that points to that prototype.

🔮 **Today & future:** Even when you use `class`, prototypes work underneath, which is why this comes up so often in interviews.

---

## 2️⃣6️⃣ Explain the concept of the `this` keyword in different contexts.

> 🎤 **Say:** The value of `this` depends on **how a function is called**, not where it is written. In a method call it is the object, in a constructor it is the new instance, and with `call/apply/bind` it is whatever I pass in. Arrow functions have no `this` of their own, they take it from the surrounding scope.

📖 **Detailed explanation**

| Context | What `this` is |
|---|---|
| Global (browser) | `window` (`undefined` in modules or strict mode) |
| Method call `obj.fn()` | `obj` (the object before the dot) |
| Plain function call `fn()` | `undefined` (strict) / global (non-strict) |
| Constructor `new Fn()` | The newly created object |
| `call / apply / bind` | The value you provide |
| Arrow function | `this` of the outer scope (lexical) |
| DOM event handler (regular function) | The element the event happened on |

**Normal vs arrow function:**

| Feature | Normal function | Arrow function |
|---|---|---|
| `this` | Dynamic, decided by the call site | Lexical, inherited from the surrounding scope |
| As a method | Refers to the object calling it | Uses the outer `this`, not the object |
| Constructor (`new`) | Allowed | Not allowed |
| `arguments` | Available | Not available |

🧠 **Simple analogy:** `this` is like the word "I". Its meaning depends on who is speaking. An arrow function is a person who always uses the "I" of the house where they were born rather than their own.

💻 **Code**

```javascript
const person = {
  name: "Alamin",
  regular() { return this.name; },       // "Alamin"
  arrow: () => this.name,                // outer this, not "Alamin"
  delayed() {
    setTimeout(() => console.log(this.name), 100);   // "Alamin" (arrow is lexical)
  },
};

const fn = person.regular;
fn();                                    // this is lost (undefined/global)

function Car(model) { this.model = model; }
new Car("X").model;                      // "X"
```

❓ **Follow-up:** "Why does `this` get lost when you assign a method to a variable?" → Because it is no longer called as `obj.fn()`, so the call site changed. Fix it with `bind` or an arrow function.

🔮 **Today & future:** Hooks reduced `this` complexity in React, but the core concept is still tested in interviews.

---

## 2️⃣7️⃣ What are JavaScript modules (import/export)?

> 🎤 **Say:** A module lets me split code into separate files, `export` what is needed and `import` it elsewhere. Each module has its own scope, so nothing pollutes the global namespace. A file can have many named exports and one default export. CommonJS `require` runs at runtime, whereas ES Modules are static, which makes tree-shaking possible.

📖 **Detailed explanation**

| Aspect | ES Modules (ESM) | CommonJS (CJS) |
|---|---|---|
| Syntax | `import` / `export` | `require()` / `module.exports` |
| Loading | Static (analyzed ahead of time) | Dynamic (at runtime) |
| Tree-shaking | Possible | Hard |
| Top-level `this` | `undefined` | `module.exports` |
| Default mode | Strict | Non-strict |

- **Named export:** many per file, imported with the exact name (`{ add }`)
- **Default export:** one per file, imported under any name
- **Live bindings:** imported values stay connected to the original
- **Dynamic import:** `const m = await import("./x.js")` (load on demand)
- In Node.js, use `"type": "module"` in `package.json` or `.mjs` files to run ESM

🧠 **Simple analogy:** Separate toolboxes. You borrow only the tool you need from another box (`import`) and put what you want to share outside your own box (`export`).

💻 **Code**

```javascript
// math.js
export const add = (a, b) => a + b;
export const PI = 3.14;
export default function sub(a, b) { return a - b; }

// app.js
import sub, { add, PI as pi } from "./math.js";
import * as math from "./math.js";     // everything at once

const { default: lazy } = await import("./math.js"); // dynamic
```

❓ **Follow-up:** "What is tree-shaking?" → Removing unused exports from the final bundle, which is possible because ESM is static.

🔮 **Today & future:** New projects (Next.js, Vite, Node ESM) run entirely on ES Modules.

---

## 2️⃣8️⃣ What is the difference between shallow copy and deep copy of objects?

> 🎤 **Say:** A shallow copy duplicates only the top level, so nested objects still share the same reference and changing one changes the other. A deep copy duplicates everything independently. Spread and `Object.assign` are shallow, and for a deep copy `structuredClone()` is now the best choice.

📖 **Detailed explanation**

| Method | Type | Limitation |
|---|---|---|
| Spread `{ ...obj }`, `[...arr]` | Shallow | Nested values are shared |
| `Object.assign({}, obj)` | Shallow | Nested values are shared |
| `arr.slice()` | Shallow | Nested values are shared |
| `structuredClone(obj)` | **Deep** | Cannot copy functions or DOM nodes |
| `JSON.parse(JSON.stringify(obj))` | Deep (limited) | Breaks `Date`, `undefined`, functions, `Map`, `Set` |
| lodash `cloneDeep` | Deep | External library |

🧠 **Simple analogy:** A shallow copy is a photocopy of a book where the picture pages are still glued to the original. A deep copy is printing the whole book again.

💻 **Code**

```javascript
const original = { name: "A", address: { city: "Sherpur" } };

const shallow = { ...original };
shallow.address.city = "Dhaka";
console.log(original.address.city);   // "Dhaka" (it changed!)

const deep = structuredClone(original);
deep.address.city = "Sylhet";
console.log(original.address.city);   // "Dhaka" (untouched)

// Problems with the JSON trick
JSON.parse(JSON.stringify({ d: new Date(), u: undefined, f() {} }));
// { d: "2026-..." } (Date became a string, u and f disappeared)
```

❓ **Follow-up:** "What can't `structuredClone` copy?" → Functions and DOM nodes.

🔮 **Today & future:** `structuredClone` is available in all modern browsers and Node, so the JSON trick is rarely needed now.

---

## 2️⃣9️⃣ What are WeakMap and WeakSet and when would you use them?

> 🎤 **Say:** WeakMap and WeakSet accept only objects and hold them **weakly**. If nothing else references an object, the garbage collector can remove it, so they do not cause memory leaks. They are not iterable and have no `size`. I use them to attach private or cached data to objects.

📖 **Detailed explanation**

| Aspect | `Map` / `Set` | `WeakMap` / `WeakSet` |
|---|---|---|
| Allowed keys | Any value | Objects only |
| Reference | Strong | Weak |
| Garbage collection | Keeps keys alive | Removed when no other reference exists |
| Iteration | Possible | Not possible |
| `size` | Yes | No |

**Uses:**
1. Storing private data for objects
2. Metadata or cache for DOM nodes (when the node is removed, the data goes too)
3. A WeakSet to track objects already seen (for example, avoiding circular references)

🧠 **Simple analogy:** A Map is a notebook that never forgets anyone. A WeakMap is a notebook where a person's entry is automatically erased once they leave town.

💻 **Code**

```javascript
const meta = new WeakMap();

let el = { id: 1 };
meta.set(el, { clicks: 0 });
meta.get(el).clicks++;       // 1
el = null;                   // the entry can now be garbage collected

// WeakSet
const visited = new WeakSet();
function walk(node) {
  if (visited.has(node)) return;   // avoids circular references
  visited.add(node);
}

// Private data with WeakMap
const priv = new WeakMap();
class User {
  constructor(pass) { priv.set(this, { pass }); }
  check(p) { return priv.get(this).pass === p; }
}
```

❓ **Follow-up:** "Why can't a WeakMap be iterated?" → Because the garbage collector decides when entries disappear, so a stable list cannot exist.

🔮 **Today & future:** In large apps, WeakMap is a professional choice for caches and metadata without memory leaks.

---

## 3️⃣0️⃣ Explain the concept of memoization with an example.

> 🎤 **Say:** Memoization means caching a function's results so that when the same input comes again, I return the stored result instead of recomputing it. It is only safe for pure functions. It saves a lot of time on expensive calculations, at the cost of some memory.

📖 **Detailed explanation**

- The cache key is the arguments, and the value is the result
- Check the cache first: if found, return it, otherwise compute, store and return
- **Requirement:** the function must be pure (same input → same output, no side effects)
- **Risks:** the cache can grow without limit (you need a size cap or LRU), and building keys with `JSON.stringify` is not safe for every kind of data

🧠 **Simple analogy:** Memorizing the multiplication table. Instead of calculating every time, you just recall the answer.

💻 **Code**

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

const slowSquare = n => { /* heavy work */ return n * n; };
const fastSquare = memoize(slowSquare);
fastSquare(9);  // computed
fastSquare(9);  // served from the cache

// Fibonacci: time goes from O(2^n) to O(n)
const fib = memoize(n => (n < 2 ? n : fib(n - 1) + fib(n - 2)));
fib(40);
```

❓ **Follow-up:** "What is the difference between memoization and caching?" → Memoization is a specific kind of caching: storing a function's results keyed by its arguments.

🔮 **Today & future:** React's `useMemo`, `useCallback` and `React.memo` apply this same idea, so it is useful for performance work in production.

---

## ✅ Last-minute checklist before the interview

- [ ] I can explain destructuring and spread/rest with examples
- [ ] I know `map`, `filter`, `reduce` and how `reduce` behaves with and without `initialValue`
- [ ] I can explain the event loop order of microtasks versus tasks
- [ ] I can explain Promises, async/await and when to use `Promise.all`
- [ ] I can describe `this` in different contexts and `call/apply/bind`
- [ ] I know shallow versus deep copy and `structuredClone`
