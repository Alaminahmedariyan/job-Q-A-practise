# 🟣 JavaScript Fundamentals II — Short Interview Answers (English)

**Topic:** Arrays, Objects, ES6+ & Async

> Every question has three parts: 🎤 **How to say it**, 📌 **Key points**, 🔮 **Today & the future**.

---

## 1️⃣6️⃣ What is destructuring? Explain with array and object examples.

> 🎤 **Say:** Destructuring is a concise way to pull values out of an array or object into separate variables. With arrays it works by position, and with objects it works by property name. It also supports default values, renaming and nested extraction, which keeps code short and readable.

📌 **Key points**
- Array → by position, Object → by name
- Defaults: `{ role = "user" }`
- Rename: `{ name: userName }`
- Works in function parameters too

```javascript
let [a, b] = [1, 2];
const { name, age = 20, city: town } = { name: "Alamin", city: "Sherpur" };
[a, b] = [b, a];              // swap
```

🔮 **Today & future:** `const [state, setState] = useState()` and props destructuring are everyday React code.

---

## 1️⃣7️⃣ What are the spread and rest operators?

> 🎤 **Say:** Both use `...` but do opposite jobs. Spread expands an array or object into individual items, and rest collects many items into one array or object. I use spread to copy and merge, and rest to accept any number of function arguments. One thing to remember: spread makes a shallow copy.

📌 **Key points**
- Spread: expands (copy, merge, pass arguments)
- Rest: collects (always the last parameter)
- Copies are shallow, nested objects keep the same reference

```javascript
const merged = [...[1, 2], ...[3, 4]];
const user2 = { ...user, role: "admin" };
const sum = (...nums) => nums.reduce((a, b) => a + b, 0);
```

🔮 **Today & future:** Spread is the standard way to update React state immutably.

---

## 1️⃣8️⃣ What is the difference between map(), filter() and reduce()?

> 🎤 **Say:** All three return a result without mutating the original array. `map` transforms each element and returns a new array of the same length. `filter` keeps only elements that pass a test. `reduce` boils the whole array down to a single value, like a sum.

📌 **Key points**
- `map` → transform (same length)
- `filter` → select (shorter or equal)
- `reduce` → single value
- `reduce` callback: `(accumulator, currentValue, currentIndex, array)`
- Without `initialValue`, the first element becomes the accumulator and iteration starts at the second
- `reduce` on an empty array with no `initialValue` throws a `TypeError`

```javascript
const nums = [1, 2, 3, 4];
nums.map(n => n * 2);                // [2, 4, 6, 8]
nums.filter(n => n % 2 === 0);       // [2, 4]
nums.reduce((acc, n) => acc + n, 0); // 10
```

🔮 **Today & future:** Chaining these three is the foundation of modern data processing and React list rendering.

---

## 1️⃣9️⃣ What is the difference between for...in and for...of?

> 🎤 **Say:** `for...in` loops over an object's enumerable property **names (keys)**, including inherited ones. `for...of` loops over the **values** of an iterable such as an array, string, Map or Set. For arrays I use `for...of`, and for plain objects I use `Object.entries()` with `for...of`.

📌 **Key points**
- `for...in` → keys (strings), includes the prototype chain
- `for...of` → values, works on iterables
- `for...of` does not work on plain objects

```javascript
for (const i in ["a", "b"]) console.log(i);   // "0", "1"
for (const v of ["a", "b"]) console.log(v);   // "a", "b"
for (const [k, v] of Object.entries({ x: 1 })) console.log(k, v);
```

🔮 **Today & future:** Modern code prefers `Object.entries()` with `for...of` or array methods.

---

## 2️⃣0️⃣ What are template literals and tagged templates?

> 🎤 **Say:** Template literals are strings written with backticks that allow `${}` expressions and multi-line text. In a tagged template, a function receives the string pieces and the values separately, so you can process them however you like. styled-components and GraphQL's `gql` work exactly this way.

📌 **Key points**
- `${expression}` for interpolation
- Multi-line strings work directly
- Tagged: first argument is the strings array, the rest are the values

```javascript
const name = "Alamin";
const msg = `Hello, ${name}! 2 + 3 = ${2 + 3}`;

function tag(strings, ...values) {
  return strings[0] + values[0].toUpperCase() + strings[1];
}
tag`Hi ${name}!`;   // "Hi ALAMIN!"
```

🔮 **Today & future:** Tagged templates are still widely used in CSS-in-JS and GraphQL libraries.

---

## 2️⃣1️⃣ What is the event loop?

> 🎤 **Say:** JavaScript is single-threaded, yet it handles async work through the event loop. When the call stack is empty, the loop first drains the **microtask queue** (Promises), then picks one task from the **task queue** (setTimeout, events). That is why a Promise callback always runs before a setTimeout callback.

📌 **Key points**
- Call stack → where code runs
- Web/Node APIs → handle timers and network
- Microtask queue (Promises) → **higher priority**
- Task queue (setTimeout) → runs later

```javascript
console.log("1");
setTimeout(() => console.log("2"), 0);
Promise.resolve().then(() => console.log("3"));
console.log("4");
// 1, 4, 3, 2
```

🔮 **Today & future:** Understanding the event loop is essential to avoid freezing the UI and to debug async bugs.

---

## 2️⃣2️⃣ How do Promises work?

> 🎤 **Say:** A Promise represents a result that will be available in the future. It has three states: pending, fulfilled and rejected. `.then()` handles success, `.catch()` handles failure and `.finally()` always runs. You can chain them, and use `Promise.all` to run many in parallel.

📌 **Key points**
- States: pending → fulfilled / rejected
- `Promise.all` → fails if any one fails
- `Promise.allSettled` → returns every outcome
- `Promise.race` → first one to settle

```javascript
fetch("/api/user")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err))
  .finally(() => console.log("done"));
```

🔮 **Today & future:** Every modern API (fetch, Prisma, SDKs) returns Promises.

---

## 2️⃣3️⃣ What is async/await and how does it improve on Promises?

> 🎤 **Say:** async/await is syntax built on top of Promises so async code reads like synchronous code. An `async` function always returns a Promise, and `await` pauses until a Promise settles. Errors are handled with plain `try/catch`, and the code is far easier to read.

📌 **Key points**
- `await` works inside `async` functions (top-level too in modules)
- Use `Promise.all` for independent tasks
- `await` inside `forEach` does not work as expected

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

🔮 **Today & future:** async/await is the standard in Node.js, Next.js and virtually all backend code.

---

## 2️⃣4️⃣ What is the difference between call(), apply() and bind()?

> 🎤 **Say:** All three let me set a function's `this` explicitly. `call` runs the function immediately with arguments passed one by one. `apply` does the same but takes arguments as an array. `bind` does not run the function, it returns a new function with `this` locked in.

📌 **Key points**
- `call(thisArg, a, b)` → runs now
- `apply(thisArg, [a, b])` → runs now, takes an array
- `bind(thisArg, a)` → returns a new function
- Arrow functions ignore these for `this`

```javascript
function hi(g) { return g + ", " + this.name; }
const u = { name: "Alamin" };
hi.call(u, "Hello");     // "Hello, Alamin"
hi.apply(u, ["Hello"]);  // same
const f = hi.bind(u);    // new function
```

🔮 **Today & future:** Arrow functions reduced the need for `bind`, but it still appears in classes and legacy code.

---

## 2️⃣5️⃣ What is prototypal inheritance?

> 🎤 **Say:** In JavaScript every object has a hidden link to another object called its prototype. If a property is not found, the engine follows that chain upward until it finds it or reaches `null`. That is the prototype chain, and the `class` syntax is simply sugar over it.

📌 **Key points**
- Every object has a `[[Prototype]]`
- Lookup follows the chain and ends at `null`
- `Object.create(proto)` inherits directly
- `class` / `extends` = syntax sugar over prototypes

```javascript
const animal = { eat() { return "eating"; } };
const dog = Object.create(animal);
dog.bark = () => "woof";
dog.eat();   // found on the prototype
```

🔮 **Today & future:** Even with `class`, prototypes work underneath, so interviewers ask about this constantly.

---

## 2️⃣6️⃣ Explain the `this` keyword in different contexts.

> 🎤 **Say:** The value of `this` depends on **how a function is called**, not where it is written. In a method call it is the object, in a constructor it is the new instance, and with `call/apply/bind` it is whatever I pass. Arrow functions have no `this` of their own, they take it from the surrounding scope.

📌 **Key points**
- Global → `window` (browser), `undefined` in modules/strict mode
- Method call → the object before the dot
- Plain function call → `undefined` (strict) or global
- `new` → the newly created object
- Arrow → lexical (from the outer scope)

```javascript
const p = {
  name: "A",
  regular() { return this.name; },     // "A"
  arrow: () => this.name,              // outer this, not "A"
};
```

🔮 **Today & future:** Hooks reduced `this` complexity in React, but the core concept is still tested in interviews.

---

## 2️⃣7️⃣ What are JavaScript modules (import/export)?

> 🎤 **Say:** A module lets me split code into files, `export` what is needed and `import` it elsewhere. Each module has its own scope, so nothing pollutes the global namespace. A file can have many named exports and one default export. Unlike CommonJS `require`, which runs at runtime, ES Modules are static, which enables tree-shaking.

📌 **Key points**
- Named export: `export const a`, import: `{ a }`
- Default export: one per file, any import name
- Dynamic import: `await import("./x.js")`
- ESM = static, CommonJS = dynamic (`require`)

```javascript
// math.js
export const add = (a, b) => a + b;
export default function sub(a, b) { return a - b; }

// app.js
import sub, { add } from "./math.js";
```

🔮 **Today & future:** New projects (Next.js, Vite, Node ESM) run entirely on ES Modules.

---

## 2️⃣8️⃣ What is the difference between shallow copy and deep copy?

> 🎤 **Say:** A shallow copy duplicates only the top level, so nested objects still share the same reference and changing one changes the other. A deep copy duplicates everything independently. Spread and `Object.assign` are shallow, and for a deep copy `structuredClone()` is now the best choice.

📌 **Key points**
- Shallow: spread, `Object.assign`, `slice`
- Deep: `structuredClone()`, lodash `cloneDeep`
- `JSON.parse(JSON.stringify())` breaks Dates, `undefined`, functions and Maps

```javascript
const a = { n: { x: 1 } };
const s = { ...a };           // shallow
s.n.x = 99;                   // a.n.x is 99 too
const d = structuredClone(a); // deep
```

🔮 **Today & future:** `structuredClone` is available in all modern browsers and Node, so the JSON trick is rarely needed.

---

## 2️⃣9️⃣ What are WeakMap and WeakSet and when would you use them?

> 🎤 **Say:** WeakMap and WeakSet only accept objects and hold them **weakly**. If nothing else references an object, the garbage collector can remove it, so they do not cause memory leaks. They are not iterable and have no `size`. I use them to attach private or cached data to objects.

📌 **Key points**
- Keys must be objects
- Garbage-collection friendly
- Not iterable, no `size`
- Uses: private data, DOM node metadata, tracking visited objects

```javascript
const meta = new WeakMap();
let el = {};
meta.set(el, { clicks: 0 });
el = null;   // the entry can now be garbage collected
```

🔮 **Today & future:** In large apps, WeakMap is a professional choice for caches and metadata without memory leaks.

---

## 3️⃣0️⃣ What is memoization? Give an example.

> 🎤 **Say:** Memoization means caching a function's results so that when the same input comes again, I return the stored result instead of recomputing it. It is only safe for pure functions. It saves a lot of time on expensive calculations, at the cost of some memory.

📌 **Key points**
- Cache key = arguments, value = result
- Only safe for pure functions
- Risk: the cache can grow without bound

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

🔮 **Today & future:** React's `useMemo`, `useCallback` and `React.memo` apply this same idea.
