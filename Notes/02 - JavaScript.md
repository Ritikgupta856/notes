# JavaScript — Complete Interview Preparation Guide

## Table of Contents

1. [JavaScript Fundamentals](#1-javascript-fundamentals)
2. [Variables & Data Types](#2-variables--data-types)
3. [Type Conversion](#3-type-conversion)
4. [Operators](#4-operators)
5. [Control Flow](#5-control-flow)
6. [Functions](#6-functions)
7. [Scope](#7-scope)
8. [Hoisting](#8-hoisting)
9. [Execution Context & Call Stack](#9-execution-context--call-stack)
10. [Closures](#10-closures)
11. [this Keyword](#11-this-keyword)
12. [Objects](#12-objects)
13. [Arrays](#13-arrays)
14. [Strings](#14-strings)
15. [Numbers & Dates](#15-numbers--dates)
16. [Error Handling](#16-error-handling)
17. [ES6+ Features](#17-es6-features)
18. [DOM](#18-dom)
19. [Events](#19-events)
20. [Asynchronous JavaScript](#20-asynchronous-javascript)
21. [Event Loop](#21-event-loop)
22. [Memory & Performance](#22-memory--performance)
23. [Browser APIs & Storage](#23-browser-apis--storage)
24. [Advanced JavaScript](#24-advanced-javascript)
25. [Senior-Level Questions](#25-senior-level-questions)
26. [Rapid-Fire Interview Questions](#26-rapid-fire-interview-questions)

---

## 1. JavaScript Fundamentals

### Version 1 (Detailed)

**What is JavaScript?**

**JavaScript** is a programming language originally built to make static web pages interactive and dynamic. Today it also runs on servers (Node.js), mobile apps, and more.

A **JavaScript engine** is a program built into web browsers (or runtimes like Node.js) that **parses and executes** JavaScript code.

Common JS engines:
- **V8** — Chrome, Node.js, Edge (Chromium-based)
- **SpiderMonkey** — Firefox
- **JavaScriptCore (Nitro)** — Safari
- **Chakra** — Old Edge (pre-Chromium)

**What are Client and Server?** (From Part 1 only)

- **Client**: a device, browser, or application that **requests and consumes** services/resources (e.g., your browser).
- **Server**: a device or application that **provides** services, resources, or data to clients (e.g., an API backend).

```
Client (Browser) ----request----> Server
Client (Browser) <---response---- Server (HTML, JSON, files, etc.)
```

### Version 2 (Quick Reference)

**What is JavaScript?**
**Answer:** JavaScript is a high-level, dynamic, single-threaded programming language mainly used to build interactive web applications. Today it is used not only in browsers but also on servers, mobile apps, desktop apps, and even tooling.

**Why was JavaScript created?**
**Answer:** JavaScript was created to add interactivity to web pages. Initially, websites were mostly static, so JavaScript was introduced to handle things like form validation, DOM updates, and event-driven behavior directly in the browser.

**What are the features of JavaScript?**
**Answer:** JavaScript is dynamically typed, prototype-based, event-driven, interpreted or JIT-compiled depending on the engine, single-threaded by nature, and supports first-class functions, closures, asynchronous programming, and object-oriented as well as functional programming styles.

**Advantages of JavaScript?**
**Answer:** Its biggest advantages are that it runs in every modern browser, has a huge ecosystem, supports both frontend and backend development, enables fast UI interactivity, and has a lower barrier to entry compared to many other languages.

**Limitations of JavaScript?**
**Answer:** JavaScript can be harder to maintain in very large codebases without strong standards, it has some historical quirks, floating-point precision issues, and because it is single-threaded, CPU-heavy work can block execution unless handled through workers or background processes.

**JavaScript vs ECMAScript?**
**Answer:** JavaScript is the actual programming language used in browsers and runtimes, while ECMAScript is the official specification or standard that defines how the language should behave.

**What is ECMAScript?**
**Answer:** ECMAScript is the standardized specification for scripting languages like JavaScript. It defines language syntax, types, objects, functions, and standard behavior.

**What is a JavaScript Engine?**
**Answer:** A JavaScript engine is the program that reads, compiles, and executes JavaScript code. Examples include V8 in Chrome and Node.js, SpiderMonkey in Firefox, and JavaScriptCore in Safari.

**What is V8 Engine?**
**Answer:** V8 is Google's JavaScript engine written in C++. It powers Chrome and Node.js, and it improves performance by converting JavaScript into optimized machine code.

**How does JavaScript work internally?**
**Answer:** Internally, JavaScript code is parsed, converted into an abstract syntax tree, compiled by the engine, and then executed inside a runtime environment. The runtime also provides APIs like timers, DOM, or file handling, and asynchronous behavior is coordinated through the event loop.

**Is JavaScript interpreted or compiled?**
**Answer:** Modern JavaScript is both. Earlier it was often described as interpreted, but modern engines like V8 use just-in-time compilation, so JavaScript is parsed and compiled into machine code during execution.

**What is JIT Compilation?**
**Answer:** JIT, or just-in-time compilation, means the engine compiles JavaScript into machine code at runtime instead of fully interpreting it line by line, which improves performance significantly.

**Browser vs Node.js?**
**Answer:** In the browser, JavaScript is mainly used for UI and DOM interaction. In Node.js, JavaScript runs on the server and provides access to file systems, networking, and backend functionality. The language is the same, but the runtime APIs are different.

**JavaScript Runtime?**
**Answer:** A JavaScript runtime is the environment where JavaScript executes. It includes the engine plus additional APIs and mechanisms like the event loop, timers, DOM APIs in browsers, or file and network APIs in Node.js.

**What is strict mode?**
**Answer:** Strict mode is a way to enable a stricter version of JavaScript by writing `"use strict"`. It prevents some unsafe behavior, catches common mistakes, and makes the code more predictable.

---

## 2. Variables & Data Types

### Version 1 (Detailed)

**Variables — Difference between `var`, `let`, and `const` ⭐ (Very Important)**

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Scope | Function-scoped | Block-scoped | Block-scoped |
| Re-declaration | Allowed | Not allowed | Not allowed |
| Re-assignment | Allowed | Allowed | **Not allowed** |
| Hoisting | Hoisted, initialized as `undefined` | Hoisted but in "temporal dead zone" | Hoisted but in "temporal dead zone" |

```js
function example() {
  if (true) {
    var a = 10;   // function-scoped — visible outside the if block
    let b = 20;   // block-scoped — only visible inside the if block
    const c = 30; // block-scoped, cannot be reassigned
  }
  console.log(a); // 10
  // console.log(b); // ReferenceError
  // console.log(c); // ReferenceError
}

const obj = { name: "Ritik" };
obj.name = "Dev"; // ✅ allowed — we're mutating the object, not reassigning the variable
// obj = {}; // ❌ TypeError — cannot reassign a const
```

**Rule of thumb:** Use `const` by default, `let` when you need to reassign, and avoid `var` in modern code.

**What are Data Types in JS?**

```
Data Types
├── Primitive (store single value, immutable)
│    ├── Number
│    ├── String
│    ├── Boolean
│    ├── Undefined
│    ├── Null
│    ├── Symbol
│    └── BigInt
└── Non-Primitive / Reference (can hold collections, mutable)
     ├── Object
     ├── Array
     ├── Function
     └── RegExp
```

```js
let y;
console.log(y); // undefined
console.log(typeof y); // "undefined"
```

**Primitive vs Non-Primitive Data Types**

| Primitive | Non-Primitive (Reference) |
|---|---|
| Holds a single value | Can hold multiple values/collections |
| Immutable — value can't be changed once created | Mutable — contents can be changed |
| Stored directly in memory (stack) | Stored as a reference (pointer) to memory (heap) |
| Examples: Number, String, Boolean | Examples: Object, Array, Function |

```js
let oddNumbers = [1, 3, 5]; // array — non-primitive

let person = {
  name: "Ritik",
  age: 23,
  grades: ["A", "B", "C"],
  greet: function () {
    console.log(this.name);
  },
};
```

**`undefined` vs `null`**

```js
let undefinedVariable;
console.log(undefinedVariable); // undefined

let nullVariable = null;
console.log(nullVariable); // null
```

- **`undefined`**: A variable has been declared but **not yet assigned** a value — JS sets this automatically.
- **`null`**: An **intentional** assignment representing "no value" — the developer explicitly sets it.

### Version 2 (Quick Reference)

**var vs let vs const?**
**Answer:** `var` is function-scoped and can be redeclared, which often causes bugs. `let` is block-scoped and can be reassigned but not redeclared in the same scope. `const` is also block-scoped but cannot be reassigned after initialization.

**What is variable hoisting?**
**Answer:** Hoisting means variable and function declarations are moved to the top of their scope during the memory creation phase. With `var`, the variable is initialized as `undefined`, while `let` and `const` remain in the temporal dead zone until declared.

**What are primitive data types?**
**Answer:** Primitive data types in JavaScript are `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol`, and `null`.

**What are reference types?**
**Answer:** Reference types are values stored by reference rather than by actual value. Common examples are objects, arrays, functions, maps, sets, and dates.

**Undefined vs Null?**
**Answer:** `undefined` means a variable has been declared but not assigned a value. `null` is an intentional assignment that represents the absence of a value.

**Symbol?**
**Answer:** `Symbol` is a primitive data type used to create unique identifiers. It is often used for object property keys where uniqueness is important.

**BigInt?**
**Answer:** `BigInt` is a primitive type used to represent integers larger than the safe limit of the regular `number` type.

**typeof operator?**
**Answer:** The `typeof` operator returns the type of a value as a string, such as `"string"`, `"number"`, or `"object"`. One known quirk is that `typeof null` returns `"object"`.

**Dynamic typing?**
**Answer:** JavaScript is dynamically typed, which means variable types are determined at runtime and a variable can hold different types of values at different times.

**Mutable vs Immutable?**
**Answer:** Mutable values can be changed after creation, like objects and arrays. Immutable values cannot be changed, like strings, numbers, booleans, `null`, and `undefined`.

---

## 3. Type Conversion

### Version 1 (Detailed)

**What is Type Coercion in JS?**

**Type coercion** is the automatic conversion of a value from one data type to another, usually during operations or comparisons.

```js
console.log("5" + 5);   // "55"  → number coerced to string (concatenation)
console.log("5" - 1);   // 4     → string coerced to number (subtraction)
console.log("5" == 5);  // true  → loose equality coerces types before comparing
```

Used mainly in:
- String + Number concatenation
- Comparison operators (`==`)

**`==` vs `===`**

```js
console.log(1 == "1");  // true  — loose equality, type coercion happens
console.log(1 === "1"); // false — strict equality, no coercion, types must match
```

- **`==` (Loose Equality)**: compares values **after** converting them to the same type.
- **`===` (Strict Equality)**: compares both **value and type**, no conversion.

✅ Best practice: prefer `===` for predictable, bug-free comparisons.

### Version 2 (Quick Reference)

**Implicit coercion?**
**Answer:** Implicit coercion is automatic type conversion done by JavaScript during operations. For example, when using `==` or adding a string with a number, JavaScript may convert one type to another automatically.

**Explicit conversion?**
**Answer:** Explicit conversion means the developer intentionally converts a value using functions like `Number()`, `String()`, or `Boolean()`.

**Truthy and Falsy values?**
**Answer:** Falsy values are values that become `false` in a boolean context, such as `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, and `NaN`. Everything else is truthy.

**== vs ===?**
**Answer:** `==` checks loose equality and performs type coercion if needed. `===` checks strict equality and compares both value and type, so in interviews I always say `===` is generally preferred for predictable behavior.

**Boolean conversion?**
**Answer:** Boolean conversion means converting a value to `true` or `false`, either explicitly with `Boolean(value)` or implicitly in conditions like `if`, `while`, or logical operators.

**String conversion?**
**Answer:** String conversion means converting a value into a string, using `String(value)`, template literals, or sometimes concatenation with an empty string, though `String()` is clearer.

**Number conversion?**
**Answer:** Number conversion means converting a value to a number using `Number()`, `parseInt()`, or `parseFloat()` depending on the use case.

**NaN?**
**Answer:** `NaN` stands for Not a Number. It represents an invalid numeric result, for example when converting a non-numeric string into a number.

**isNaN() vs Number.isNaN()?**
**Answer:** `isNaN()` first coerces the value, which can lead to misleading results. `Number.isNaN()` is stricter and returns true only if the value is actually `NaN`.

**Object to primitive conversion?**
**Answer:** When JavaScript needs a primitive from an object, it tries methods like `valueOf()` and `toString()`. The exact behavior depends on the operation being performed.

---

## 4. Operators

### Version 1 (Detailed)

**Operators and Types of Operators ⭐ (Very Important)**

```
Types of Operators
├── Arithmetic   (+, -, *, /, %, **)
├── Assignment   (=, +=, -=, *=, /=)
├── Comparison   (==, ===, !=, !==, >, <, >=, <=)
├── Logical      (&&, ||, !)
└── String       (+ for concatenation)
```

```js
let x = 10, y = 5;

// Arithmetic
console.log(x + y); // 15
console.log(x - y); // 5
console.log(x * y); // 50
console.log(x / y); // 2
console.log(x % y); // 0 (remainder)
console.log(x ** y); // 100000 (exponentiation)

// Assignment
x += 5; // same as x = x + 5
console.log(x); // 15

// Comparison
console.log(x > y);   // true
console.log(x < y);   // false
console.log(x >= y);  // true
console.log(x <= y);  // false
console.log(x === y); // false (strict equality)
console.log(x !== y); // true

// Logical
console.log(x && y); // truthy && truthy -> y (5)
console.log(x || y); // truthy || truthy -> x (15)
console.log(!x);     // false

// String concatenation
let a = "Hello", b = "World";
console.log(a + " " + b); // "Hello World"
```

**Unary, Binary, and Ternary Operators**

| Type | Operands | Example |
|---|---|---|
| Unary | 1 | `++a`, `-a`, `!a` |
| Binary | 2 | `a + b`, `a * b` |
| Ternary | 3 | `condition ? a : b` |

```js
let a = 5;
console.log(++a); // 6 (unary)

let b = a + 10;   // binary
console.log(b);

let result = a > 5 ? "big" : "small"; // ternary
console.log(result);
```

**What is Short-Circuit Evaluation in JS?**

JS **stops evaluating** an expression as soon as the final result is already determined.

```js
function someFunction() {
  console.log("I ran!");
  return true;
}

let result1 = false && someFunction();
console.log(result1); // false — someFunction() never runs (&& short-circuits on first falsy)

let result2 = true || someFunction();
console.log(result2); // true — someFunction() never runs (|| short-circuits on first truthy)
```

**Operator Precedence**

Operators with **higher precedence** are evaluated first.

```js
console.log(2 + 3 * 4);   // 14 — multiplication before addition
console.log((2 + 3) * 4); // 20 — parentheses override precedence
```

General order (high to low, simplified): `()` → `**` → `* / %` → `+ -` → comparison → logical → assignment.

**Spread vs Rest Operator**

Both use `...` but work in **opposite directions**.

**Spread (`...`)** — expands an iterable into individual elements.
```js
let arr = [1, 2, 3];
console.log(...arr); // 1 2 3

let copy = [...arr];              // copy an array
let merged = [...arr, 4, 5];      // merge arrays

function sum(a, b, c, d, e) {
  console.log(a + b + c + d + e);
}
let numbers = [1, 2, 3, 4, 5];
sum(...numbers); // spreads array into individual arguments
```

**Rest (`...`)** — collects remaining arguments into an array.
```js
function display(first, second, ...rest) {
  console.log(first);  // 1
  console.log(second); // 2
  console.log(rest);   // [3, 4, 5]
}
display(1, 2, 3, 4, 5);
```

### Version 2 (Quick Reference)

**Spread Operator?**
**Answer:** The spread operator `...` expands elements of an iterable or properties of an object. It is commonly used to copy arrays, merge objects, or pass multiple arguments.

**Rest Operator?**
**Answer:** The rest operator also uses `...`, but it collects multiple values into a single array or object, such as in function parameters or destructuring.

**Nullish Coalescing?**
**Answer:** The nullish coalescing operator `??` returns the right-hand value only when the left-hand value is `null` or `undefined`. It does not treat `0` or an empty string as missing.

**Optional Chaining?**
**Answer:** Optional chaining `?.` lets us safely access nested properties or methods without throwing an error if part of the chain is `null` or `undefined`.

**Ternary Operator?**
**Answer:** The ternary operator is a concise conditional expression written as `condition ? valueIfTrue : valueIfFalse`.

**Logical Operators?**
**Answer:** The main logical operators are `&&`, `||`, and `!`. They are used for boolean logic, but in JavaScript they also return actual operand values, not always just true or false.

**Short-circuit evaluation?**
**Answer:** Short-circuiting means JavaScript stops evaluating an expression once the result is already determined. For example, with `&&`, if the first value is falsy, the second is not evaluated.

**Bitwise Operators?**
**Answer:** Bitwise operators work at the binary level, such as `&`, `|`, `^`, `~`, `<<`, `>>`, and `>>>`. They are less common in day-to-day frontend work but useful in low-level operations.

**delete operator?**
**Answer:** The `delete` operator removes a property from an object. It does not delete variables declared with `var`, `let`, or `const`.

**in operator?**
**Answer:** The `in` operator checks whether a property exists in an object, including inherited properties.

---

## 5. Control Flow

### Version 1 (Detailed)

**Types of Conditional Statements ⭐ (Very Important)**

```
1. if / else if / else
2. Ternary operator (condition ? a : b)
3. switch statement
```

```js
// 1. if/else
let num = 10;
if (num > 0) {
  console.log("Positive");
} else if (num < 0) {
  console.log("Negative");
} else {
  console.log("Zero");
}

// 2. Ternary
let result = num > 0 ? "Positive" : "Not Positive";
console.log(result);

// 3. switch
switch (num) {
  case 10:
    console.log("It's ten");
    break;
  default:
    console.log("Unknown");
}
```

**if/else vs Ternary vs switch — When to Use Each**

| Statement | Best for |
|---|---|
| `if...else` | Complex, multi-condition, multi-line logic |
| Ternary | Simple, single-value conditional assignment |
| `switch` | Comparing one value against many fixed possibilities |

- **if/else** → covers all scenarios, most flexible.
- **Ternary** → short, one-line syntax for simple decisions.
- **switch** → cleaner, more structured code when checking the same variable against many values.

**What is a Loop? Types of Loops in JS**

A **loop** repeatedly executes a block of code until a condition is no longer met.

```
JavaScript Loops
├── for
├── while
├── do...while
├── for...in   (iterates object keys)
└── for...of   (iterates iterable values — arrays, strings, etc.)
```

```js
for (let i = 0; i < 3; i++) console.log(i);   // 0, 1, 2

let i = 0;
while (i < 3) { console.log(i); i++; }        // 0, 1, 2

let j = 0;
do { console.log(j); j++; } while (j < 3);    // 0, 1, 2 (runs at least once)
```

**`break` vs `continue` ⭐ (Very Important)**

```js
for (let i = 0; i < 5; i++) {
  if (i === 3) break; // exits the loop entirely
  console.log(i);
}
// Output: 0, 1, 2

for (let i = 0; i < 5; i++) {
  if (i === 3) continue; // skips just this iteration
  console.log(i);
}
// Output: 0, 1, 2, 4
```

- **`break`**: terminates the loop completely.
- **`continue`**: skips the current iteration and moves to the next.

**`for` Loop vs `for...of` Loop**

```js
let arr = ["a", "b", "c"];

// for loop — more code, gives you the index
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

// for...of — simpler, gives you the value directly
for (let value of arr) {
  console.log(value);
}
```

`for...of` is simpler and preferred for iterating over arrays when you just need the values.

**`for...of` vs `for...in` ⭐ (Very Important)**

```js
let person = {
  name: "Happy",
  role: "Developer",
};

// for...of works on iterables (arrays, strings) — NOT plain objects directly
let arr = ["Happy", "Developer"];
for (let value of arr) {
  console.log(value); // "Happy", "Developer"
}

// for...in iterates over the KEYS of an object
for (let key in person) {
  console.log(key, person[key]); // "name Happy", "role Developer"
}
```

| | `for...of` | `for...in` |
|---|---|---|
| Iterates over | Values (arrays, strings, iterables) | Keys/property names (objects) |
| Best used with | Arrays, strings, Maps, Sets | Plain objects |

**`forEach()` vs `for...of` vs `for...in` ⭐ (Very Important)**

```js
let person = { name: "Happy", role: "Developer" };
let arr = ["Happy", "Developer"];

// for...in — object keys
for (let key in person) {
  console.log(key);
}

// for...of — array values
for (let item of arr) {
  console.log(item);
}

// forEach — array method, callback-based
arr.forEach((item) => {
  console.log(item);
});

// Object.values() + for...of — object values
for (let value of Object.values(person)) {
  console.log(value);
}
```

**`forEach()`** is a **method available on arrays** that iterates over each element and runs a callback on it.

**When to use what:**
- Use **`for...of`** when you need control over the loop — e.g., using `break` or `continue` mid-iteration (forEach can't be stopped early).
- Use **`forEach()`** when you simply want to perform an action on every element with no need to exit early.
- Use **`for...in`** specifically for iterating over an object's own enumerable property keys.

---

## 6. Functions

### Version 1 (Detailed)

**Functions in JS — Types of Functions**

```
Types of Functions
├── Named Function
├── Anonymous Function
├── Function Expression
├── Arrow Function
├── IIFE (Immediately Invoked Function Expression)
├── Callback Function
└── Higher-Order Function
```

```js
// Named function
function add(a, b) { return a + b; }

// Anonymous function (assigned to a variable)
const sub = function (a, b) { return a - b; };

// Arrow function
const mul = (a, b) => a * b;

// IIFE — runs immediately, doesn't pollute global scope
(function () {
  console.log("IIFE executed");
})();

// Callback — a function passed into another function
function greet(name, callback) {
  callback(name);
}
greet("Ritik", (name) => console.log(`Hello, ${name}`));

// Higher-order function — takes/returns a function
function multiplyBy(factor) {
  return (num) => num * factor;
}
const double = multiplyBy(2);
console.log(double(5)); // 10
```

**Named vs Anonymous Functions — When to Use What**

```js
// Named function — has its own identifier, can be called by name, supports recursion
function sum(a, b) {
  return a + b;
}
console.log(sum(5, 3)); // 8

// Anonymous function — no name, usually assigned to a variable or passed inline
const multiply = function (a, b) {
  return a * b;
};
console.log(multiply(5, 3)); // 15
```

| | Named Functions | Anonymous Functions |
|---|---|---|
| Has identifier | Yes | No |
| Can self-reference (recursion) | Yes | Only if assigned to a variable first |
| Best for | Big, reusable, complex logic used in multiple places | Small, one-off logic used in a single place |

**Function Expression in JS**

A **function expression** defines a function by assigning it to a variable, rather than declaring it with the `function` keyword on its own.

```js
const add = function (a, b) {
  return a + b;
};
console.log(add(5, 3)); // 8
```

Unlike function **declarations**, function expressions are **not hoisted** — you can't call `add()` before this line runs.

**What are Callback Functions? What is their use? ⭐ (Very Important)**

A **callback function** is a function passed as an **argument** to another function, to be invoked later.

```js
function add(a, b) { return a + b; }
function subtract(a, b) { return a - b; }
function multiply(a, b) { return a * b; }
function divide(a, b) { return a / b; }

// display() is the higher-order function, the math functions are callbacks
function display(a, b, callback) {
  console.log(callback(a, b));
}

display(10, 5, add);      // 15
display(10, 5, subtract); // 5
display(10, 5, multiply); // 50
display(10, 5, divide);   // 2
```

Callbacks are the foundation of async JS — used heavily in event handlers, `setTimeout`, array methods, and (historically) async operations before Promises.

**What is a Higher-Order Function in JS?**

A **higher-order function** either:
1. Takes one or more functions as arguments (a callback), **or**
2. **Returns** a function as its result.

```js
// Takes a callback function
function hof(func) {
  func();
}
function sayHello() {
  console.log("Hello!");
}
hof(sayHello); // "Hello!"

// Returns a function
function createAdder(number) {
  return function (value) {
    return value + number;
  };
}
const addFive = createAdder(5);
console.log(addFive(2)); // 7
```

`map()`, `filter()`, and `reduce()` are all built-in higher-order functions since they accept a callback.

**Parameters vs Arguments**

- **Parameters**: the placeholder names defined in a function's declaration.
- **Arguments**: the actual values passed in when the function is called.

```js
function greet(name) { // "name" is the parameter
  console.log("Hello " + name);
}
greet("Ritik"); // "Ritik" is the argument
```

**Ways to Pass Arguments to a Function**

```
Ways to Pass Arguments
├── Positional Arguments  — order matters
├── Named Arguments       — pass an object, access by key
└── Arguments Object      — access all args via `arguments`
```

```js
// Positional arguments
function add(a, b) {
  console.log(a + b);
}
add(3, 4); // 7

// Named arguments (using an object)
function greet(person) {
  console.log(person.name + " is a " + person.role);
}
greet({ name: "Ritik", role: "Developer" });

// Arguments object — only in regular functions, not arrow functions
function sum() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  console.log(total);
}
sum(1, 2, 3); // 6
```

**Default Parameters in a Function**

Default parameters let you specify a fallback value if no argument (or `undefined`) is passed.

```js
function greet(name = "Friend") {
  console.log("Hello " + name + "!");
}

greet("Amit"); // "Hello Amit!"
greet();       // "Hello Friend!"
```

**First-Class Functions in JS**

A language has **first-class functions** if functions are treated like any other value — they can be:

```
1. Assigned to variables
2. Passed as arguments to other functions
3. Returned as values from other functions
```

```js
// 1. Assignable
const myFunction = function () {
  console.log("I'm a value!");
};

// 2. Passable as arguments
function performOperation(operation, value) {
  return operation(value);
}
const double = (value) => value * 2;
console.log(performOperation(double, 5)); // 10

// 3. Returnable as values
function createSimpleFunction() {
  return function () {
    console.log("I am from the returned function.");
  };
}
const simpleFunction = createSimpleFunction();
simpleFunction(); // "I am from the returned function."
```

**Pure vs Impure Functions**

```js
// Pure function — same input always gives same output, no side effects
function add(a, b) {
  return a + b;
}
console.log(add(3, 5)); // 8
console.log(add(3, 5)); // 8 (always the same)

// Impure function — depends on / modifies external state
let total = 0;
function addToTotal(value) {
  total += value;
  return total;
}
console.log(addToTotal(5)); // 5
console.log(addToTotal(5)); // 10 (different output for same input!)
```

- **Pure function**: always produces the same output for the same input, and has no side effects.
- **Impure function**: can produce different outputs for the same input because it relies on or changes external state.

**Function Currying in JS**

**Currying** transforms a function that takes multiple arguments into a series of nested functions, each taking a single argument.

```js
// Normal function with multiple arguments
function multiply(a, b) {
  return a * b;
}

// Curried version
function curriedMultiply(a) {
  return function (b) {
    return a * b;
  };
}

const double = curriedMultiply(2);
console.log(double(5)); // 10

const triple = curriedMultiply(3);
console.log(triple(5)); // 15
```

**Advantages**: reusability, modularity, and specialization — big functions with many arguments can be broken into small, reusable, single-argument functions.

**`call`, `apply`, and `bind` Methods**

These three methods control **what `this` refers to** when a function is invoked, and let you pass arguments explicitly.

```js
function sayHello(greeting) {
  console.log(greeting + ", " + this.name);
}

const person = { name: "Ritik" };

// call() — invokes immediately, arguments passed individually
sayHello.call(person, "Hello"); // "Hello, Ritik"

// apply() — invokes immediately, arguments passed as an array
sayHello.apply(person, ["Hi"]); // "Hi, Ritik"

// bind() — returns a NEW function with `this` bound, doesn't invoke immediately
const greetPerson = sayHello.bind(person, "Greetings");
greetPerson(); // "Greetings, Ritik"
```

| Method | Invokes immediately? | Arguments format |
|---|---|---|
| `call()` | Yes | Individual values |
| `apply()` | Yes | Array |
| `bind()` | No — returns a new function | Individual values |

### Version 2 (Quick Reference)

**Function Declaration?**
**Answer:** A function declaration defines a named function using the `function` keyword and is hoisted completely, so it can be called before its declaration.

**Function Expression?**
**Answer:** A function expression stores a function inside a variable. It can be named or anonymous, and unlike function declarations, it is not fully hoisted with its implementation.

**Arrow Functions?**
**Answer:** Arrow functions are a shorter syntax for writing functions. They do not have their own `this`, `arguments`, or `prototype`, so they are best for callbacks and lexical `this` behavior.

**Anonymous Functions?**
**Answer:** Anonymous functions are functions without a name. They are often used as callbacks or assigned to variables.

**Named Functions?**
**Answer:** Named functions are functions that have an explicit name. They are useful for debugging, recursion, and clearer stack traces.

**IIFE?**
**Answer:** IIFE stands for Immediately Invoked Function Expression. It is a function that runs immediately after being defined, often used earlier to create private scope.

**Callback Functions?**
**Answer:** A callback is a function passed into another function to be executed later, often after some event or asynchronous operation completes.

**Higher Order Functions?**
**Answer:** A higher-order function is a function that takes another function as an argument or returns a function. Examples include `map`, `filter`, and `reduce`.

**First Class Functions?**
**Answer:** JavaScript functions are first-class citizens, which means they can be assigned to variables, passed as arguments, returned from other functions, and stored in data structures.

**Pure Functions?**
**Answer:** A pure function always returns the same output for the same input and does not produce side effects like modifying external variables or making API calls.

**Generator Functions?**
**Answer:** Generator functions are special functions defined with `function*` that can pause and resume execution using the `yield` keyword.

**Recursive Functions?**
**Answer:** A recursive function is a function that calls itself until a base condition is met.

**Constructor Functions?**
**Answer:** Constructor functions are regular functions used with the `new` keyword to create object instances before ES6 classes became common.

**Factory Functions?**
**Answer:** Factory functions are functions that return objects directly, without needing `new`. They are often simpler and more flexible than constructor functions.

**Default Parameters?**
**Answer:** Default parameters let us assign fallback values to function parameters if no argument or `undefined` is passed.

---

## 7. Scope

### Version 1 (Detailed)

**What is Scope in JavaScript?**

**Scope** determines where a variable is accessible from in your code.

```
Scope Types
├── Global Scope    — accessible everywhere
├── Function Scope  — accessible only inside the function
└── Block Scope     — accessible only inside { } (let/const only)
```

```js
let globalVariable = "I'm global";

function greet() {
  let functionVariable = "I'm function-scoped";

  if (true) {
    let blockVariable = "I'm block-scoped";
    console.log(blockVariable);     // ✅ works
    console.log(functionVariable);  // ✅ works
    console.log(globalVariable);    // ✅ works
  }

  // console.log(blockVariable); // ❌ ReferenceError — out of scope
  console.log(functionVariable);    // ✅ works
  console.log(globalVariable);      // ✅ works
}

greet();
console.log(globalVariable); // ✅ works
// console.log(functionVariable); // ❌ ReferenceError
```

**Lexical Scoping ⭐ (Very Important)**

**Lexical scoping** means a function's access to variables is determined by **where it is physically written in the code**, not where it's called from. Inner functions can access variables from their outer (parent) scope.

```js
function outerFunction() {
  let outerVariable = "I'm from outer scope";

  function innerFunction() {
    console.log(outerVariable); // accessible due to lexical scoping
  }

  innerFunction();
}

outerFunction(); // "I'm from outer scope"
```

### Version 2 (Quick Reference)

**Global Scope?**
**Answer:** Variables declared outside any function or block are in global scope and can be accessed from anywhere in the program, though excessive global scope is generally discouraged.

**Function Scope?**
**Answer:** Variables declared with `var` inside a function are accessible only within that function.

**Block Scope?**
**Answer:** Variables declared with `let` and `const` inside a block like an `if` or loop are only accessible within that block.

**Lexical Scope?**
**Answer:** Lexical scope means scope is determined by where variables and functions are written in the source code, not by where they are called from.

**Scope Chain?**
**Answer:** The scope chain is the sequence of nested scopes JavaScript follows when resolving a variable, starting from the current scope and moving outward to parent scopes.

**Shadowing?**
**Answer:** Shadowing happens when a variable in an inner scope has the same name as a variable in an outer scope, so the inner one hides the outer one within that scope.

**Illegal Shadowing?**
**Answer:** Illegal shadowing happens when JavaScript disallows a conflicting declaration, such as declaring `let` inside a block when a `var` with the same name exists in a conflicting scope.

**Variable Lifetime?**
**Answer:** Variable lifetime refers to how long a variable exists in memory. Local variables usually live for the duration of execution context, while closed-over variables can live longer if referenced by closures.

---

## 8. Hoisting

### Version 1 (Detailed)

**What is Hoisting in JavaScript?**

**Hoisting** means JS moves function and variable **declarations** to the top of their scope during the compilation phase, before the code actually runs.

```js
// Function hoisting — works even before the declaration
myFunction(); // "Hello!"

function myFunction() {
  console.log("Hello!");
}

// Variable hoisting with var
console.log(myVar); // undefined (not an error — but also not "Hello")
var myVar = "Hello";

// let/const are hoisted too, but stay in the "temporal dead zone"
// console.log(myLet); // ❌ ReferenceError
let myLet = "Hi";
```

### Version 2 (Quick Reference)

**What is hoisting?**
**Answer:** Hoisting is JavaScript's behavior of moving declarations to the top of their scope during the memory creation phase before code execution starts.

**How var hoisting works?**
**Answer:** `var` declarations are hoisted and initialized with `undefined`, so they can be accessed before declaration without a ReferenceError, though the value will be `undefined`.

**How let hoisting works?**
**Answer:** `let` is also hoisted, but it is not initialized during the early phase. It stays in the temporal dead zone until the declaration line is reached.

**Temporal Dead Zone?**
**Answer:** The temporal dead zone is the period between entering a scope and the point where a `let` or `const` variable is declared, during which accessing it throws a ReferenceError.

**Function hoisting?**
**Answer:** Function declarations are fully hoisted, so they can be called before they appear in the code. Function expressions are not hoisted the same way.

**Class hoisting?**
**Answer:** Classes are hoisted, but like `let` and `const`, they remain in the temporal dead zone until the class declaration is evaluated.

---

## 9. Execution Context & Call Stack

### Version 2 Only

**What is Execution Context?**
**Answer:** Execution context is the environment in which JavaScript code is evaluated and executed. It contains information about variables, functions, and the value of `this`.

**Global Execution Context?**
**Answer:** The global execution context is the default context created when the script first runs. It sets up the global object, global variables, and `this`.

**Function Execution Context?**
**Answer:** A new function execution context is created each time a function is invoked. It contains that function's local variables, arguments, inner declarations, and `this` binding.

**Memory Creation Phase?**
**Answer:** In the memory creation phase, JavaScript allocates memory for variables and functions before executing the code. Function declarations get their full definitions, while variables are initialized depending on how they are declared.

**Execution Phase?**
**Answer:** In the execution phase, JavaScript runs the code line by line, assigns variable values, executes function calls, and evaluates expressions.

**Call Stack?**
**Answer:** The call stack is the data structure JavaScript uses to keep track of execution contexts. When a function is called, it is pushed onto the stack, and when it returns, it is popped off.

---

## 10. Closures

### Version 1 (Detailed)

**What is a Closure?**

A **closure** is the combination of a function and the **lexical environment** it was created in — it "remembers" the variables from its outer scope even after that outer function has finished executing.

```js
function outerFunction() {
  let count = 0;

  function innerFunction() {
    count++;
    console.log(count);
  }

  return innerFunction;
}

const closure = outerFunction();
closure(); // 1
closure(); // 2 — count persists between calls!
```

**Benefits of Closures ⭐ (Very Important)**

```
Benefits of Closures
├── Data Privacy (Encapsulation) — variables stay hidden from outside access
├── Persistent Data and State    — each closure keeps its own private state
└── Code Reusability             — the returned function can be reused freely
```

```js
function createCounter() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}

const counter1 = createCounter();
console.log(counter1()); // 1
console.log(counter1()); // 2

const counter2 = createCounter();
console.log(counter2()); // 1 — counter2 has its OWN separate `count`, unaffected by counter1
```

This is the classic example: each call to `createCounter()` creates a brand-new, **private** `count` variable that only the returned function can access — that's data encapsulation via closures.

### Version 2 (Quick Reference)

**What is Closure?**
**Answer:** A closure is created when a function remembers and accesses variables from its lexical scope even after the outer function has finished executing.

**Why closures exist?**
**Answer:** Closures exist because JavaScript uses lexical scoping. Inner functions keep access to the variables of their outer scope as long as they are still referenced.

**Real-world uses?**
**Answer:** Closures are used for data privacy, function factories, event handlers, callbacks, memoization, currying, and maintaining state between function calls.

**Advantages?**
**Answer:** Closures help with encapsulation, state preservation, reusable function generation, and cleaner abstraction patterns.

**Disadvantages?**
**Answer:** If misused, closures can increase memory usage, retain unnecessary references, and make debugging more difficult.

**Memory leaks due to closures?**
**Answer:** Closures can cause memory leaks if they keep references to large objects or DOM elements that are no longer needed, preventing garbage collection.

**Closure interview examples?**
**Answer:** A classic example is a function returning another function that increments a private counter. The inner function continues to access the counter even after the outer function has returned.

---

## 11. this Keyword

### Version 2 Only

**What is this?**
**Answer:** `this` is a special keyword that refers to the execution context of a function, and its value depends on how the function is called.

**this in global scope?**
**Answer:** In browsers, outside strict mode, `this` in global scope refers to the `window` object. In strict mode it depends on context, and in modules it behaves differently.

**this in function?**
**Answer:** In a regular function, `this` depends on how the function is invoked. In non-strict mode, a standalone function call defaults to the global object in browsers; in strict mode it is `undefined`.

**this in object?**
**Answer:** In an object method, `this` usually refers to the object before the dot that called the method.

**this in arrow function?**
**Answer:** Arrow functions do not have their own `this`. They inherit `this` lexically from the surrounding scope.

**call()?**
**Answer:** `call()` invokes a function immediately and lets us specify the value of `this`, followed by arguments individually.

**apply()?**
**Answer:** `apply()` works like `call()`, but it accepts arguments as an array or array-like object.

**bind()?**
**Answer:** `bind()` does not execute the function immediately. It returns a new function with `this` permanently bound to the provided value.

**call vs apply vs bind?**
**Answer:** `call` and `apply` both invoke the function immediately, with the difference being how arguments are passed. `bind` returns a new function and is used when I want to reuse the bound function later.

---

## 12. Objects

### Version 1 (Detailed)

**What are Objects in JS? ⭐ (Important)**

An **object** is a data type that stores data as **key-value pairs**. Values can be strings, numbers, booleans, arrays, other objects, or even functions.

```js
let person = {
  name: "Happy",
  age: 25,
  hobbies: ["Teaching", "Football", "Coding"],
  greet: function () {
    console.log("Name: " + this.name);
  },
};

console.log("Name: " + person.name);      // dot notation
console.log(person["name"]);              // bracket notation
console.log(person.hobbies[1]);            // "Football"
person.greet();                            // "Name: Happy"
```

**Ways to Iterate Over the Properties of an Object**

```js
const person = { name: "Ritik", role: "Developer", age: 23 };

// 1. for...in
for (let key in person) {
  console.log(key, person[key]);
}

// 2. Object.keys()
Object.keys(person).forEach((key) => console.log(key, person[key]));

// 3. Object.values()
Object.values(person).forEach((value) => console.log(value));

// 4. Object.entries()
Object.entries(person).forEach(([key, value]) => console.log(key, value));
```

**Shallow Copy vs Deep Copy ⭐ (Very Important)**

```js
const person = {
  name: "Ritik",
  age: 25,
  address: { city: "Jaipur", country: "India" },
};

// Shallow copy — nested objects are shared by reference
const shallowCopy = Object.assign({}, person);
shallowCopy.address.city = "Mumbai";
console.log(person.address.city);       // "Mumbai" — changed too! Same nested reference
console.log(shallowCopy.address.city);  // "Mumbai"

// Deep copy — fully independent, nested objects are cloned too
const deepCopy = JSON.parse(JSON.stringify(person));
deepCopy.address.city = "Delhi";
console.log(person.address.city);    // "Mumbai" — unaffected
console.log(deepCopy.address.city);  // "Delhi"
```

- **Shallow copy**: copies only the top-level properties. Nested objects are still **shared references** — modifying a nested value affects the original too.
- **Deep copy**: recursively clones everything, including nested objects, so the copy is fully independent.

⚠️ `JSON.parse(JSON.stringify())` works for simple objects but **loses functions, `undefined`, `Date` objects, and `Symbol`s**. For complex cases, use `structuredClone()` (modern browsers/Node) or a library like Lodash's `cloneDeep()`.

**Add, Modify, or Delete Properties of an Object**

```js
const person = { name: "Ritik" };

// Add
person.age = 25;
person["role"] = "Developer";

// Modify
person.name = "Ritik Sharma";

// Delete
delete person.role;

console.log(person); // { name: "Ritik Sharma", age: 25 }
```

**Dot Notation vs Bracket Notation**

```js
const person = { name: "Ritik", "favorite-color": "blue" };

console.log(person.name);              // dot notation — simple and common
console.log(person["name"]);           // bracket notation — same result

console.log(person["favorite-color"]); // ✅ works — dot notation CAN'T be used here (hyphen)
// console.log(person.favorite-color);  // ❌ invalid syntax

const key = "name";
console.log(person[key]); // ✅ bracket notation lets you use a variable as the key
```

**Dot notation** is simpler and more common, but **bracket notation** is required when:
- The property name is stored in a variable
- The property name has spaces, hyphens, or starts with a number

**Ways to Create an Object**

```js
// 1. Object literal
const obj1 = { name: "Ritik" };

// 2. Using `new Object()`
const obj2 = new Object();
obj2.name = "Ritik";

// 3. Using a constructor function
function Person(name) {
  this.name = name;
}
const obj3 = new Person("Ritik");

// 4. Using Object.create()
const obj4 = Object.create(null);
obj4.name = "Ritik";

// 5. Using a class
class PersonClass {
  constructor(name) {
    this.name = name;
  }
}
const obj5 = new PersonClass("Ritik");
```

### Version 2 (Quick Reference)

**Object Creation?**
**Answer:** Objects can be created using object literals, constructor functions, classes, `Object.create()`, or factory functions.

**Object Literals?**
**Answer:** Object literals are the most common way to create objects, using curly braces with key-value pairs.

**Constructor Objects?**
**Answer:** Constructor functions create object instances using the `new` keyword, which sets up `this`, links the prototype, and returns the object.

**Object.assign()?**
**Answer:** `Object.assign()` copies enumerable properties from one or more source objects into a target object. It performs a shallow copy.

**Object.freeze()?**
**Answer:** `Object.freeze()` prevents adding, deleting, or modifying properties on an object. It is shallow, so nested objects can still be mutable unless frozen separately.

**Object.seal()?**
**Answer:** `Object.seal()` prevents adding or deleting properties, but existing properties can still be modified unless they are non-writable.

**Object.keys()?**
**Answer:** `Object.keys()` returns an array of an object's own enumerable property names.

**Object.values()?**
**Answer:** `Object.values()` returns an array of an object's own enumerable property values.

**Object.entries()?**
**Answer:** `Object.entries()` returns an array of key-value pairs for an object's own enumerable properties.

**hasOwnProperty()?**
**Answer:** `hasOwnProperty()` checks whether a property exists directly on the object rather than being inherited through the prototype chain.

**Object Destructuring?**
**Answer:** Object destructuring is a syntax that extracts properties from an object into variables in a concise way.

**Optional Chaining?**
**Answer:** Optional chaining safely accesses nested object properties or methods without throwing if an intermediate value is null or undefined.

---

## 13. Arrays

### Version 1 (Detailed)

**Arrays — Getting, Adding & Removing Elements ⭐ (Very Important)**

```
Array Methods
├── Get      → indexOf(), includes(), find(), filter(), slice()
├── Add      → push(), unshift(), concat(), splice()
├── Remove   → pop(), shift(), splice()
├── Modify   → map(), sort(), reverse(), splice()
└── Others   → forEach(), reduce(), some(), every(), length
```

```js
let arr = [1, 2, 3];

arr.push(4);       // [1, 2, 3, 4] — add to end
arr.pop();         // [1, 2, 3]    — remove from end
arr.unshift(0);    // [0, 1, 2, 3] — add to start
arr.shift();       // [1, 2, 3]    — remove from start

let filtered = arr.filter(n => n > 1); // [2, 3]
let mapped = arr.map(n => n * 2);      // [2, 4, 6]

let merged = [1, 2].concat([3, 4]);    // [1, 2, 3, 4]
```

**`indexOf()` Method of an Array**

Returns the index of the **first match** of a given element, or `-1` if not found.

```js
let arr = [10, 20, 30, 40];
console.log(arr.indexOf(30)); // 2
console.log(arr.indexOf(99)); // -1
```

**`find()` vs `filter()` ⭐ (Very Important)**

```js
let nums = [1, 2, 3, 4, 5, 6];

let c = nums.find(num => num % 2 === 0);
console.log(c); // 2 — first matching element only

let d = nums.filter(num => num % 2 === 0);
console.log(d); // [2, 4, 6] — array of ALL matching elements
```

- **`find()`**: returns the **first single element** that satisfies a condition.
- **`filter()`**: returns an **array of all elements** that satisfy a condition.

**`slice()` Method of an Array**

Returns a **subset** of an array from `start` index to `end` index (end **not included**) — does not modify the original array.

```js
let arr = [1, 2, 3, 4, 5];
let e = arr.slice(1, 3);
console.log(e);   // [2, 3]
console.log(arr); // [1, 2, 3, 4, 5] — unchanged
```

**`push()` vs `concat()`**

```js
let array1 = [1, 2];
array1.push(3, 4);
console.log(array1); // [1, 2, 3, 4] — original array IS modified

let array2 = [1, 2];
let newArray = array2.concat([3, 4]);
console.log(array2);   // [1, 2] — original unchanged
console.log(newArray); // [1, 2, 3, 4] — a brand-new array
```

- **`push()`** mutates the original array.
- **`concat()`** creates and returns a new array, leaving the original untouched.

**`pop()` vs `shift()`**

```js
let arr1 = [1, 2, 3, 4];
let last = arr1.pop();
console.log(arr1); // [1, 2, 3] — last element removed
console.log(last);  // 4

let arr2 = [1, 2, 3, 4];
let first = arr2.shift();
console.log(arr2); // [2, 3, 4] — first element removed
console.log(first); // 1
```

**`splice()` Method of an Array**

Used to **add, remove, or replace** elements in an array — modifies the array in place.

```js
let letters = ["a", "b", "c", "d", "e"];

// splice(startIndex, deleteCount)
letters.splice(1, 2);
console.log(letters); // ["a", "d", "e"]

// splice(startIndex, deleteCount, ...itemsToInsert)
letters.splice(2, 1, "q");
console.log(letters); // ["a", "d", "q"]
```

**`slice()` vs `splice()`**

| | `slice()` | `splice()` |
|---|---|---|
| Mutates original? | No | Yes |
| Purpose | Extract a portion | Add/remove/replace elements |
| Returns | New array (the extracted portion) | Array of removed elements |

**`map()` vs `forEach()`**

```js
let arr1 = [1, 2, 3];
let mapArray = arr1.map(e => e * 2);
console.log(mapArray); // [2, 4, 6] — new array returned

let arr2 = [1, 2, 3];
arr2.forEach(e => console.log(e * 2)); // 2, 4, 6 — just runs side effects
```

- **`map()`**: transforms each element and **returns a new array**.
- **`forEach()`**: performs an action on each element but **returns `undefined`** — used for side effects only.

**Sorting and Reversing an Array**

```js
let array = [3, 1, 4, 1, 5];

array.sort();
console.log(array); // [1, 1, 3, 4, 5] (sorts as strings by default!)

array.sort((a, b) => a - b); // correct numeric ascending sort
console.log(array); // [1, 1, 3, 4, 5]

array.reverse();
console.log(array); // [5, 4, 3, 1, 1]
```

⚠️ Note: `sort()` without a comparator sorts elements as **strings**, which can give wrong results for numbers (e.g., `10` comes before `2`). Always pass a comparator for numeric sorting.

**Array Destructuring**

Lets you extract elements from an array into individual variables in one statement.

```js
let array1 = [1, 2, 3];
let [a, b, c] = array1;
console.log(a, b, c); // 1 2 3

// Skipping elements
let [first, , third] = array1;
console.log(first, third); // 1 3

// With default values
let [x = 10, y = 20] = [5];
console.log(x, y); // 5 20
```

**Array-Like Objects in JS ⭐ (Very Important)**

**Array-like objects** have indexed elements and a `length` property, similar to arrays — but they **don't have array methods** like `push()` or `pop()`.

```
Types of Array-Like Objects
├── arguments object (inside regular functions)
├── Strings
└── HTMLCollections (e.g., from getElementsByClassName)
```

```js
function example() {
  console.log(arguments.length); // works
  // arguments.push(1); // ❌ TypeError — no push method
}
example(1, 2, 3);

const boxes = document.getElementsByClassName("box"); // HTMLCollection — array-like
```

**Converting an Array-Like Object into a Real Array**

```js
function example() {
  // Method 1: Array.from()
  let array1 = Array.from(arguments);
  console.log(array1);

  // Method 2: Spread syntax
  let array2 = [...arguments];
  console.log(array2);

  // Method 3: Array.prototype.slice.call()
  let array3 = Array.prototype.slice.call(arguments);
  console.log(array3);
}
example(1, 2, 3);
```

All three give you a real array with full access to `.map()`, `.filter()`, `.push()`, etc.

**Arrays vs Objects**

| | Arrays | Objects |
|---|---|---|
| Structure | Collection of values | Collection of key-value pairs |
| Syntax | Square brackets `[]` | Curly braces `{}` |
| Order | Ordered (indexed) | Unordered (key-based) |
| Best for | Lists of similar items | Structured data with named properties |

### Version 2 (Quick Reference)

**map()?**
**Answer:** `map()` creates a new array by transforming every element of the original array using a callback.

**filter()?**
**Answer:** `filter()` creates a new array containing only the elements that satisfy a given condition.

**reduce()?**
**Answer:** `reduce()` processes an array and accumulates it into a single result, such as a sum, object, or flattened structure.

**forEach()?**
**Answer:** `forEach()` executes a callback for each array element but does not return a new transformed array.

**find()?**
**Answer:** `find()` returns the first element that matches a condition, or `undefined` if none matches.

**some()?**
**Answer:** `some()` returns true if at least one array element satisfies the condition.

**every()?**
**Answer:** `every()` returns true only if all elements satisfy the condition.

**includes()?**
**Answer:** `includes()` checks whether an array contains a specific value and returns a boolean.

**slice()?**
**Answer:** `slice()` returns a shallow copy of a portion of an array without modifying the original array.

**splice()?**
**Answer:** `splice()` modifies the original array by adding, removing, or replacing elements at a given index.

**concat()?**
**Answer:** `concat()` merges arrays or values into a new array without mutating the originals.

**flat()?**
**Answer:** `flat()` creates a new array with nested arrays flattened up to a specified depth.

**flatMap()?**
**Answer:** `flatMap()` first maps each element and then flattens the result by one level.

**sort()?**
**Answer:** `sort()` sorts array elements in place. By default it sorts as strings, so for numbers I provide a compare function.

**reverse()?**
**Answer:** `reverse()` reverses the order of an array in place.

**Array.from()?**
**Answer:** `Array.from()` creates an array from array-like or iterable values, and it can also apply a mapping function.

**Array.of()?**
**Answer:** `Array.of()` creates a new array from the arguments passed to it.

**Difference between map and forEach?**
**Answer:** `map()` returns a new transformed array, while `forEach()` is mainly for side effects and returns `undefined`.

**map vs filter vs reduce?**
**Answer:** `map()` transforms elements, `filter()` selects elements, and `reduce()` combines elements into a single output.

---

## 14. Strings

### Version 1 (Detailed)

**Important String Operations in JS**

Common string methods:

| Method | Purpose |
|---|---|
| `charAt()` | Get character at an index |
| `charCodeAt()` | Get Unicode value of a character |
| `indexOf()` / `lastIndexOf()` | Find position of a substring |
| `includes()` | Check if string contains a substring |
| `slice()` / `substring()` / `substr()` | Extract part of a string |
| `split()` | Split string into an array |
| `concat()` | Join strings together |
| `replace()` | Replace part of a string |
| `trim()` | Remove whitespace from both ends |
| `toUpperCase()` / `toLowerCase()` | Change case |
| `search()` / `match()` | Search using regex |
| `valueOf()` / `toString()` | Convert to primitive string |

```js
let str1 = "Hello";
let str2 = "World";

let result = str1 + " " + str2;
console.log(result);              // "Hello World"
console.log(result.toUpperCase()); // "HELLO WORLD"
console.log(result.toLowerCase()); // "hello world"

let arr = result.split(" ");
console.log(arr); // ["Hello", "World"]

let result2 = str1.concat(" ", str2);
console.log(result2); // "Hello World"

let subString = result.substring(0, 5);
console.log(subString); // "Hello"

console.log(result.replace("World", "JS")); // "Hello JS"

let str = "   trim me   ";
let trimmedStr = str.trim();
console.log(trimmedStr); // "trim me"
console.log(result.length); // 11
```

**Template Literals and String Interpolation**

**Template literals** (introduced in ES6) use backticks `` ` `` and allow embedding expressions directly inside strings with `${}`, plus support multi-line strings.

```js
const name = "Ritik";
const role = "Developer";

const greeting = `Hello, my name is ${name} and I work as a ${role}.`;
console.log(greeting);

const multiLine = `Line one
Line two
Line three`;
console.log(multiLine);
```

**Ways to Concatenate Strings**

```js
let a = "Hello", b = "World";

console.log(a + " " + b);        // 1. + operator
console.log(a.concat(" ", b));   // 2. concat() method
console.log(`${a} ${b}`);        // 3. Template literals
console.log([a, b].join(" "));   // 4. Array join()
```

### Version 2 (Quick Reference)

**String methods?**
**Answer:** Common string methods include `slice`, `substring`, `toUpperCase`, `toLowerCase`, `trim`, `split`, `replace`, `includes`, `startsWith`, and `endsWith`.

**Template Literals?**
**Answer:** Template literals use backticks and allow embedded expressions with `${}`. They also support multi-line strings naturally.

**String immutability?**
**Answer:** Strings are immutable in JavaScript, which means once a string is created, it cannot be changed. String operations return new strings instead of modifying the original one.

**substring() vs slice()?**
**Answer:** Both extract parts of a string, but `slice()` supports negative indexes while `substring()` does not and also swaps arguments if start is greater than end.

**trim()?**
**Answer:** `trim()` removes whitespace from both the beginning and end of a string.

**split()?**
**Answer:** `split()` divides a string into an array based on a separator.

**replace()?**
**Answer:** `replace()` returns a new string where part of the original is replaced. It can work with strings or regular expressions.

---

## 15. Numbers & Dates

### Version 2 Only

**parseInt() vs Number()?**
**Answer:** `Number()` attempts to convert the entire value into a number, while `parseInt()` parses until it hits an invalid character and is mainly used for integers. I also usually pass a radix to `parseInt()`.

**parseFloat()?**
**Answer:** `parseFloat()` parses a string and returns a floating-point number until it reaches an invalid character.

**Math methods?**
**Answer:** Common Math methods include `Math.round`, `Math.floor`, `Math.ceil`, `Math.random`, `Math.max`, `Math.min`, `Math.abs`, and `Math.sqrt`.

**Infinity?**
**Answer:** `Infinity` is a special numeric value representing something larger than any finite number, such as the result of dividing a positive number by zero.

**Floating point precision?**
**Answer:** JavaScript uses IEEE 754 floating-point representation, so some decimal calculations like `0.1 + 0.2` produce precision issues. In financial or precision-critical code, I avoid relying directly on floating arithmetic.

**Date Object?**
**Answer:** The `Date` object is used to create, manipulate, and format dates and times in JavaScript.

**Date formatting?**
**Answer:** Dates can be formatted using methods like `toLocaleDateString`, `toISOString`, `Intl.DateTimeFormat`, or external libraries for more control.

**Timezones?**
**Answer:** JavaScript dates internally represent time as milliseconds since the Unix epoch, and display methods can show values based on local timezone or UTC depending on the method used.

---

## 16. Error Handling

### Version 1 (Detailed)

**Types of Errors in JS**

```
JavaScript Error Types
├── SyntaxError    — invalid code structure (e.g., missing bracket)
├── ReferenceError — using a variable that doesn't exist
├── TypeError      — operating on a value of the wrong type
├── RangeError     — a number is outside an allowed range
├── EvalError      — error related to the eval() function (rarely seen now)
└── URIError       — invalid usage of encodeURI()/decodeURI()
```

```js
// SyntaxError
// const x = ; // invalid syntax

// ReferenceError
// console.log(undeclaredVar);

// TypeError
// let num = 5;
// num(); // can't call a number as a function

// RangeError
// new Array(-1); // invalid array length

// Handling errors gracefully with try/catch
try {
  JSON.parse("not valid json");
} catch (error) {
  console.error(error.name, "-", error.message);
}
```

### Version 2 (Quick Reference)

**try...catch?**
**Answer:** `try...catch` is used to handle runtime errors gracefully. Code that may throw goes inside `try`, and if an error occurs, control moves to `catch`.

**finally?**
**Answer:** `finally` runs after `try` and `catch` regardless of whether an error occurred, so it is useful for cleanup work.

**throw?**
**Answer:** `throw` is used to manually create and raise an error or any value, though in real-world code I prefer throwing `Error` objects.

**Custom Errors?**
**Answer:** Custom errors are user-defined error classes, usually extending the built-in `Error` class, to represent domain-specific failures more clearly.

---

## 17. ES6+ Features

### Version 1 (Detailed)

**What is ES6? New Features Introduced**

**ECMAScript (ES6 / ES2015)** is the standardized specification that JavaScript follows. ES6 introduced major modern features:

```
ES6 Key Features
├── let and const
├── Arrow functions
├── Template literals
├── Default parameters
├── Destructuring (array & object)
├── Spread and Rest operators
├── Classes
├── Modules (import/export)
├── Promises
├── for...of loop
├── Map and Set
└── Symbol data type
```

### Version 2 (Quick Reference)

**let & const?**
**Answer:** `let` and `const` were introduced in ES6 to provide block scope and safer variable management than `var`. `let` allows reassignment, while `const` does not.

**Destructuring?**
**Answer:** Destructuring is a syntax for extracting values from arrays or properties from objects into variables.

**Spread?**
**Answer:** Spread expands iterable elements or object properties, commonly used for copying and merging.

**Rest?**
**Answer:** Rest collects remaining values into a single array or object.

**Arrow Functions?**
**Answer:** Arrow functions provide shorter syntax and lexical `this`, making them especially useful in callbacks and functional patterns.

**Template Literals?**
**Answer:** Template literals allow expression interpolation and multi-line strings using backticks.

**Modules?**
**Answer:** ES6 modules allow code to be split into reusable files using `export` and `import`, which improves maintainability and supports tree shaking.

**Classes?**
**Answer:** Classes provide a cleaner syntax over JavaScript's prototype-based inheritance. Under the hood, they still work with prototypes.

**Promises?**
**Answer:** Promises represent the eventual completion or failure of an asynchronous operation and help avoid deeply nested callbacks.

**async/await?**
**Answer:** `async/await` is syntax built on top of promises that makes asynchronous code look more like synchronous code and improves readability.

---

## 18. DOM

### Version 1 (Detailed)

**What is the DOM? Difference between static HTML and the DOM**

The **DOM (Document Object Model)** represents an HTML page as a **tree-like structure** of objects, so JavaScript can dynamically read and change the content, structure, and styling of a page.

```
<html>
 ├── <head>
 │     └── <title>My Page</title>
 └── <body>
       ├── <h1>My Header</h1>
       └── <p>My Paragraph</p>
```

- **Static HTML** is just the text file sent by the server — it doesn't change on its own.
- **The DOM** is the **live, in-memory tree** the browser builds from that HTML. JS can add, remove, or modify nodes in this tree, and the page updates instantly.

**What are Selectors in JS?**

Selectors let you grab elements from the DOM using IDs, classes, or tag names.

| Selector | Returns |
|---|---|
| `getElementById()` | Single element with matching `id` |
| `getElementsByClassName()` | Live collection of elements with matching class |
| `getElementsByTagName()` | Live collection of elements with matching tag |
| `querySelector()` | First element matching a CSS selector |
| `querySelectorAll()` | All elements matching a CSS selector (NodeList) |

```html
<p id="test">Hello</p>
```
```js
const el = document.getElementById("test");
console.log(el.innerHTML); // "Hello"
```

**`getElementById` vs `getElementsByClassName` vs `getElementsByTagName`**

```html
<div id="myDiv">
  <p class="text">First</p>
  <p class="text">Second</p>
</div>
```

```js
// By ID — returns one element
const elementById = document.getElementById("myDiv");
console.log(elementById.innerHTML);

// By class name — returns a collection, loop through it
const elements = document.getElementsByClassName("text");
for (let i = 0; i < elements.length; i++) {
  console.log(elements[i].textContent);
}

// By tag name — returns a collection
const elementsTag = document.getElementsByTagName("p");
for (let i = 0; i < elementsTag.length; i++) {
  console.log(elementsTag[i].textContent);
}
```

**Adding/Removing Styles and Properties on DOM Elements ⭐ (Important)**

```html
<div id="myElement">Hello, World!</div>
```

```js
const el = document.getElementById("myElement");

// Content
el.textContent = "Plain text only";       // no HTML parsing
el.innerHTML = "<strong>Happy</strong>";  // parses HTML tags

// Attributes
el.setAttribute("class", "highlight");
el.removeAttribute("class");

// Styles
el.style.setProperty("color", "blue");

// Classes
el.classList.add("highlight");
el.classList.remove("highlight");
el.classList.toggle("highlight");

// Custom data attributes
el.setAttribute("data-info", "new value");
```

### `innerHTML` vs `textContent` (Important)

| | `innerHTML` | `textContent` |
|---|---|---|
| Parses HTML tags? | Yes | No — treats everything as plain text |
| Security | Risk of XSS if inserting user input | Safer — no HTML execution |
| Use case | When you need to insert actual markup | When you just need plain text |

```js
el.innerHTML = "<strong>Happy</strong>"; // renders bold "Happy"
el.textContent = "<strong>Happy</strong>"; // renders the literal text "<strong>Happy</strong>"
```

**How Do You Create DOM Elements?**

```js
const newDiv = document.createElement("div");
newDiv.textContent = "Newly created div";
document.body.appendChild(newDiv);
```

**`querySelector()` vs `querySelectorAll()`**

```js
const firstMatch = document.querySelector(".item");   // returns the FIRST matching element
const allMatches = document.querySelectorAll(".item"); // returns ALL matching elements (NodeList)

allMatches.forEach((el) => console.log(el.textContent));
```

**`createElement()` vs `createTextNode()`**

```js
// createElement() — creates a new HTML element node
const newDiv = document.createElement("div");
newDiv.innerHTML = "<strong>New div</strong>";
document.body.appendChild(newDiv);

// createTextNode() — creates a plain text node (no HTML parsing)
const textNode = document.createTextNode("Just plain text");
document.body.appendChild(textNode);
```

Other ways to insert elements dynamically: `innerHTML`, `insertAdjacentHTML()`, `document.write()` (legacy, rarely recommended).

### Version 2 (Quick Reference)

**What is DOM?**
**Answer:** The DOM, or Document Object Model, is a tree-like representation of an HTML document that JavaScript can read and modify.

**DOM Tree?**
**Answer:** The DOM tree is the hierarchical structure of nodes representing elements, attributes, text, and document relationships.

**Selecting Elements?**
**Answer:** Elements can be selected using methods like `getElementById`, `getElementsByClassName`, `querySelector`, and `querySelectorAll`.

**Creating Elements?**
**Answer:** We create DOM elements using methods like `document.createElement()` and then insert them using methods such as `appendChild` or `append`.

**Removing Elements?**
**Answer:** Elements can be removed using methods like `remove()` or by removing them from their parent node.

**Event Listeners?**
**Answer:** Event listeners are functions attached to DOM elements that run when specific events occur, such as click, input, or submit.

**Event Delegation?**
**Answer:** Event delegation is a pattern where a single event listener is attached to a parent element and handles events from child elements using event bubbling.

---

## 19. Events

### Version 1 (Detailed)

**Event Handling in JS ⭐ (Very Important)**

**Event handling** is the process of responding to user actions on a web page (clicks, typing, scrolling, etc.).

`addEventListener()` attaches an event name + a handler function to an element.

```html
<button id="myButton">Click me</button>
```
```js
const button = document.getElementById("myButton");

button.addEventListener("click", () => {
  alert("Button clicked!");
});
```

Common events:

| Event | Listener |
|---|---|
| Click | `addEventListener('click', handler)` |
| Mouseover | `addEventListener('mouseover', handler)` |
| Keydown / Keyup | `addEventListener('keydown'/'keyup', handler)` |
| Submit | `addEventListener('submit', handler)` |
| Focus / Blur | `addEventListener('focus'/'blur', handler)` |
| Change | `addEventListener('change', handler)` |
| Load | `addEventListener('load', handler)` |
| Resize | `addEventListener('resize', handler)` |

**Removing an Event Handler from an Element**

```js
function handleClick() {
  console.log("Clicked!");
}

const button = document.getElementById("myButton");
button.addEventListener("click", handleClick);

// Later, remove it — note: must pass the SAME function reference
button.removeEventListener("click", handleClick);
```

⚠️ You can't remove a listener added with an anonymous inline function — you need a named reference to both add and remove it.

**Stopping Event Propagation / Bubbling**

```js
document.getElementById("child").addEventListener("click", (event) => {
  event.stopPropagation(); // stops the event from bubbling up to parent elements
  console.log("Child clicked");
});
```

**What is Event Capturing?**

**Event capturing** is the phase where an event is handled starting from the **outermost ancestor** down to the target element — the opposite direction of bubbling.

```js
document.getElementById("outer").addEventListener(
  "click",
  () => console.log("Capturing: outer"),
  true // `true` enables capturing phase instead of default bubbling
);
```

The event travel order is: **Capturing (top → target) → Target → Bubbling (target → top)**.

**What is Event Delegation? ⭐ (Important)**

**Event delegation** attaches a **single event listener to a parent element**, instead of separate listeners on each child — taking advantage of event bubbling.

```html
<ul id="list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

```js
document.getElementById("list").addEventListener("click", (event) => {
  if (event.target.tagName === "LI") {
    console.log("Clicked:", event.target.textContent);
  }
});
```

**Why it's useful**: works automatically for dynamically added children, and uses far less memory than attaching a listener to every single item.

**What is Event Bubbling?**

**Event bubbling** is when an event triggered on a child element **propagates upward**, triggering handlers on its parent elements too.

```html
<div id="outer">
  <div id="inner">
    <button id="myButton">Click Me</button>
  </div>
</div>
```

```js
document.getElementById("outer").addEventListener("click", () => console.log("Bubbling: outer"));
document.getElementById("inner").addEventListener("click", () => console.log("Bubbling: inner"));
document.getElementById("myButton").addEventListener("click", () => console.log("Bubbling: myButton"));

// Clicking the button logs all three, in this order:
// "Bubbling: myButton" → "Bubbling: inner" → "Bubbling: outer"
```

**What is the Event Object?**

Whenever an event fires, the browser automatically creates an **event object** and passes it to the handler function — it contains useful info about the event.

```js
document.getElementById("myButton").addEventListener("click", (event) => {
  console.log("Event type:", event.type);          // "click"
  console.log("Target element:", event.target);    // the clicked element
  event.preventDefault();                            // prevents default behavior (e.g., form submission)
});
```

### Version 2 (Quick Reference)

**Event Bubbling?**
**Answer:** Event bubbling means an event starts from the target element and propagates upward through its ancestors.

**Event Capturing?**
**Answer:** Event capturing is the phase where the event travels from the outermost ancestor down to the target before bubbling begins.

**stopPropagation()?**
**Answer:** `stopPropagation()` prevents the event from continuing further through the propagation path.

**preventDefault()?**
**Answer:** `preventDefault()` prevents the browser's default action, like form submission or link navigation.

**Event Delegation?**
**Answer:** Event delegation improves performance and handles dynamic elements by attaching one listener to a common ancestor instead of many listeners to child elements.

**Event Object?**
**Answer:** The event object contains details about the event, such as the target element, event type, key pressed, mouse position, and methods like `preventDefault()`.

---

## 20. Asynchronous JavaScript

### Version 1 (Detailed)

**What is Asynchronous Programming in JS? What is it used for?**

**Asynchronous programming** lets multiple operations run without blocking the main thread — the program keeps going while waiting for something slow (like a network request) to finish.

```
Used for:
├── Fetching data from an API
├── Downloading / uploading files
├── Animations and transitions
└── Any time-taking operation
```

```js
console.log("Start");

function function1() {
  setTimeout(() => console.log("Function1 done"), 1000);
}
function function2() {
  console.log(100 + 50);
}

function1();
function2();
console.log("End");

// Output order: Start, 150, End, Function1 done
// (function1's callback runs later because it's async)
```

**Synchronous vs Asynchronous Programming**

| Synchronous | Asynchronous |
|---|---|
| Tasks run one after another, in sequence | Tasks can start, run, and complete independently/in parallel |
| Each task must finish before the next starts | Doesn't wait — execution continues |
| Execution is **blocked** until a task finishes | Operations are typically **non-blocking** |
| Can cause UI freezing for slow operations | Enables better concurrency and responsiveness |
| Default mode of execution in JS | Achieved via callbacks, Promises, async/await |

**What are Promises in JavaScript? ⭐ (Very Important)**

A **Promise** represents a value that may not be available yet, but will be at some point in the future. It's a cleaner way to handle async operations than plain callbacks.

A Promise is always in one of **three states**:

```
Pending  →  the operation hasn't finished yet
Fulfilled (Resolved)  →  operation completed successfully
Rejected  →  operation failed
```

```js
const myPromise = new Promise((resolve, reject) => {
  let success = true;
  if (success) {
    resolve("Data loaded successfully!");
  } else {
    reject("Something went wrong.");
  }
});

myPromise
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

**When to Use Promises in Real Applications**

Promises are useful whenever you need to perform a **time-consuming operation asynchronously** and handle the result once it becomes available — e.g., fetching data from an API, reading a file, or querying a database.

**`Promise.all()`**

`Promise.all()` takes an **array of Promises** and waits for **all of them** to resolve. If any one rejects, the whole thing rejects immediately.

```js
const promise1 = new Promise((resolve) => setTimeout(resolve, 1000, "First"));
const promise2 = new Promise((resolve) => setTimeout(resolve, 2000, "Second"));
const promise3 = new Promise((resolve) => setTimeout(resolve, 1500, "Third"));

Promise.all([promise1, promise2, promise3])
  .then((results) => console.log(results)) // ["First", "Second", "Third"]
  .catch((error) => console.error(error));
```

**`Promise.race()`**

`Promise.race()` takes an array of Promises and resolves/rejects **as soon as the first one settles** (whichever finishes first — resolved or rejected).

```js
const promiseA = new Promise((resolve) => setTimeout(resolve, 500, "A wins"));
const promiseB = new Promise((resolve) => setTimeout(resolve, 1000, "B wins"));

Promise.race([promiseA, promiseB])
  .then((result) => console.log(result)) // "A wins" — finished first
  .catch((error) => console.error(error));
```

**`Promise.all()` vs `Promise.race()`**

| | `Promise.all()` | `Promise.race()` |
|---|---|---|
| Waits for | **All** promises to settle | **First** promise to settle |
| Use case | You need every result before continuing | You only care about whichever finishes first |
| Fails if | Any single promise rejects | The first-settling promise rejects |

**`async`/`await` vs Promises ⭐ (Very Important)**

```js
// Using Promises with .then()/.catch()
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Data received"), 1000);
  });
}

fetchData()
  .then((result) => console.log(result))
  .catch((error) => console.error(error));

// Using async/await — same logic, more readable
async function getData() {
  try {
    const result = await fetchData();
    console.log(result);
  } catch (error) {
    console.error(error);
  }
}
getData();
```

- Both achieve the same goal: handling async operations.
- `async/await` provides **more concise, readable syntax** that resembles synchronous code.
- Promises use **chaining** with `.then()`/`.catch()`, which can get harder to read with many steps.
- `async/await` still relies on Promises **under the hood**.

**The `async` and `await` Keywords**

- **`async`**: marks a function as asynchronous — it will always return a Promise, and code inside it won't block other code.
- **`await`**: pauses execution **inside an async function** until a Promise resolves (or rejects).

```js
function delay(ms) {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Done waiting!"), ms);
  });
}

async function greet() {
  console.log("Waiting...");
  const message = await delay(2000);
  console.log(message); // "Done waiting!" — after 2 seconds
}

greet();
```

⚠️ `await` can only be used **inside** an `async` function (or at the top level of modern modules).

### Version 2 (Quick Reference)

**Synchronous vs Asynchronous?**
**Answer:** Synchronous code runs line by line and blocks the next task until the current one finishes. Asynchronous code allows long-running operations to be handled without blocking the main execution flow.

**Callback?**
**Answer:** A callback is a function passed to another function to be executed later, often when an asynchronous task completes.

**Callback Hell?**
**Answer:** Callback hell happens when multiple nested callbacks make code difficult to read, debug, and maintain.

**Promise?**
**Answer:** A promise is an object representing the eventual result of an asynchronous operation, whether fulfilled or rejected.

**Promise States?**
**Answer:** A promise has three states: pending, fulfilled, and rejected.

**Promise Chaining?**
**Answer:** Promise chaining means returning promises from `.then()` handlers so async operations can run in sequence cleanly.

**async/await?**
**Answer:** `async/await` makes promise-based code easier to read by allowing us to write asynchronous logic in a sequential style.

**Promise.all()?**
**Answer:** `Promise.all()` runs multiple promises in parallel and resolves when all succeed, but rejects immediately if any one promise rejects.

**Promise.race()?**
**Answer:** `Promise.race()` settles as soon as the first promise settles, whether it resolves or rejects.

**Promise.any()?**
**Answer:** `Promise.any()` resolves as soon as the first promise fulfills, and it rejects only if all promises reject.

**Promise.allSettled()?**
**Answer:** `Promise.allSettled()` waits for all promises to settle and returns the result of each one, whether fulfilled or rejected.

---

## 21. Event Loop

### Version 1 (Detailed)

**`setTimeout()` — Handling Async Operations ⭐ (Very Important)**

`setTimeout()` schedules a function to run **once**, after a specified delay (in milliseconds), without blocking the rest of the code.

```js
console.log("Start");

setTimeout(() => {
  console.log("Time out!");
}, 2000);

console.log("End");

// Output: Start, End, (2 seconds later) Time out!
```

**`setInterval()` — Handling Async Operations**

`setInterval()` repeatedly runs a function at a fixed time interval, until stopped with `clearInterval()`.

```js
console.log("Start");

const intervalId = setInterval(() => {
  console.log("I keep running every 3 seconds");
}, 3000);

console.log("Not blocked — this runs immediately");

// To stop it later:
// clearInterval(intervalId);
```

### Version 2 (Quick Reference)

**What is Event Loop?**
**Answer:** The event loop is the mechanism that coordinates execution between the call stack, microtask queue, and callback queue so JavaScript can handle asynchronous operations despite being single-threaded.

**Microtask Queue?**
**Answer:** The microtask queue contains high-priority tasks such as promise callbacks and `queueMicrotask`, and it is processed before the next macrotask.

**Callback Queue?**
**Answer:** The callback queue, often called the macrotask queue, contains tasks such as `setTimeout`, `setInterval`, and some I/O callbacks waiting for the call stack to be free.

**Macrotasks?**
**Answer:** Macrotasks are tasks scheduled by APIs like `setTimeout`, `setInterval`, or message events. They are processed one at a time by the event loop after microtasks are cleared.

**Execution order?**
**Answer:** First synchronous code runs, then microtasks are processed, then one macrotask is taken, and after that microtasks are processed again before the next macrotask.

**setTimeout()?**
**Answer:** `setTimeout()` schedules a callback to run after a minimum delay, but the actual execution depends on when the call stack becomes available.

**setInterval()?**
**Answer:** `setInterval()` repeatedly schedules a callback at a fixed interval, though actual timing can drift if the main thread is busy.

**requestAnimationFrame()?**
**Answer:** `requestAnimationFrame()` schedules a callback before the next browser repaint, making it ideal for smooth animations.

**queueMicrotask()?**
**Answer:** `queueMicrotask()` schedules a microtask that runs after the current synchronous code but before the next macrotask.

**process.nextTick() (Node.js)?**
**Answer:** In Node.js, `process.nextTick()` schedules a callback to run before other microtasks and before the event loop continues, which gives it very high priority.

---

## 22. Memory & Performance

### Version 2 Only

**Stack vs Heap?**
**Answer:** Primitive values and execution contexts are generally managed in the stack for fast access, while reference-type objects are stored in the heap, which is a larger and less structured memory area.

**Garbage Collection?**
**Answer:** Garbage collection is the automatic process of reclaiming memory occupied by objects that are no longer reachable in the program.

**Memory Leaks?**
**Answer:** Memory leaks happen when memory that is no longer needed remains referenced and therefore cannot be garbage collected.

**WeakMap?**
**Answer:** `WeakMap` is a collection of key-value pairs where keys must be objects and are held weakly, meaning they do not prevent garbage collection.

**WeakSet?**
**Answer:** `WeakSet` is a collection of objects held weakly, useful when you want membership tracking without preventing garbage collection.

---

## 23. Browser APIs & Storage

### Version 1 (Detailed)

**Browser APIs**

**Browser APIs** are built-in interfaces provided by web browsers that let JavaScript interact with the browser and the device.

| Category | Examples |
|---|---|
| DOM API | `getElementById()`, `querySelector()`, `createElement()`, `appendChild()`, `addEventListener()` |
| XMLHttpRequest | `open()`, `send()`, `setRequestHeader()`, `onreadystatechange` |
| Fetch API | `fetch()`, `.then()`, `.json()`, `headers.get()` |
| Storage API | `localStorage`, `sessionStorage` |
| History API | `pushState()`, `replaceState()`, `go()`, `back()` |
| Geolocation API | `getCurrentPosition()`, `watchPosition()`, `clearWatch()` |
| Notifications API | `Notification.requestPermission()`, `new Notification()`, `onclick` |
| Canvas API | `getContext()`, `fillRect()`, `drawImage()`, `beginPath()` |
| Media API | `HTMLMediaElement` (`play()`, `pause()`, `currentTime`, `volume`) |

**What is Web Storage? Types of Web Storage**

**Web Storage** lets you store data **locally within the browser**.

```
Types of Web Storage
├── localStorage   — persists indefinitely
└── sessionStorage — persists only for the current tab/session
```

Common uses:
1. Storing user preferences/settings
2. Caching data to improve performance
3. Remembering user actions and state
4. Implementing offline functionality
5. Storing client-side tokens

**What is `localStorage`? How to Use It**

`localStorage` stores key-value pairs **persistently** on the user's device — data survives even after closing the browser.

```js
// Set
localStorage.setItem("username", "Ritik");

// Get
const username = localStorage.getItem("username");
console.log(username); // "Ritik"

// Remove a single item
localStorage.removeItem("username");

// Clear everything
localStorage.clear();
```

**`localStorage` vs `sessionStorage`**

| | `localStorage` | `sessionStorage` |
|---|---|---|
| Scope | Accessible across all windows/tabs of the same origin | Specific to a single tab/window |
| Persistence | Stays even after the browser is closed and reopened | Cleared when the tab/window is closed |
| Expiration | No expiration unless explicitly removed | Temporary — lasts only for the session |

**What are Cookies? Creating and Reading Them**

**Cookies** are small pieces of data stored in the browser, often sent automatically with HTTP requests (unlike `localStorage`).

```js
// Create a cookie
document.cookie = "username=Ritik; expires=Fri, 31 Dec 2026 23:59:59 GMT; path=/";

// Read all cookies and extract one by name
function getCookie(cookieName) {
  const cookies = document.cookie.split(";");
  for (let i = 0; i < cookies.length; i++) {
    const cookie = cookies[i].trim().split("=");
    if (cookie[0] === cookieName) {
      return cookie[1];
    }
  }
  return null;
}

const cookieValue = getCookie("username");
console.log(cookieValue); // "Ritik"
```

---

## 24. Advanced JavaScript

### Version 2 Only

**Prototype?**
**Answer:** Every JavaScript object has an internal link to another object called its prototype, from which it can inherit properties and methods.

**Prototype Chain?**
**Answer:** The prototype chain is the lookup path JavaScript follows when accessing a property. If the property is not found on the object itself, JavaScript looks up the chain through its prototypes.

**Classes vs Prototypes?**
**Answer:** Classes are syntactic sugar over JavaScript's prototype-based inheritance model. Under the hood, JavaScript still uses prototypes for inheritance.

**Currying?**
**Answer:** Currying is the technique of transforming a function that takes multiple arguments into a sequence of functions that each take one argument.

**Debounce vs Throttle?**
**Answer:** Debounce delays function execution until a period of inactivity has passed, while throttle ensures a function runs at most once in a specified interval.

---

## 25. Senior-Level Questions

### Explain the JavaScript execution pipeline from source code to machine code.
**Answer:** First, the engine parses the source code and creates an abstract syntax tree. Then it performs interpretation or baseline compilation, and hot code paths may be optimized further by the JIT compiler into machine code. During execution, de-optimization can also happen if runtime assumptions become invalid.

### Explain the V8 engine architecture.
**Answer:** At a high level, V8 has a parser, an interpreter, a compiler pipeline, a garbage collector, and memory management components. It parses code into an AST, generates bytecode, executes it, and optimizes hot functions into machine code for better performance.

### Explain how the Event Loop works internally.
**Answer:** JavaScript executes synchronous code on the call stack. Async APIs hand off work to the browser or runtime. Once complete, callbacks are placed into queues. The event loop checks whether the stack is empty, processes all microtasks, and then pulls the next macrotask, repeating this continuously.

### Explain the difference between Microtasks and Macrotasks with examples.
**Answer:** Microtasks have higher priority and run immediately after the current synchronous code finishes, before the browser or runtime processes the next macrotask. Promise callbacks and `queueMicrotask()` are microtasks, while `setTimeout()` and `setInterval()` are macrotasks.

### How does the Call Stack interact with the Event Loop?
**Answer:** The call stack executes synchronous code. The event loop only pushes queued callbacks into the stack when the stack is empty. That is how asynchronous callbacks eventually get executed.

### Explain closures internally.
**Answer:** Internally, when a function is created, it keeps a reference to its lexical environment. If that function outlives its outer function, the engine preserves the needed variables so the inner function can still access them later.

### Explain lexical environments.
**Answer:** A lexical environment is the internal structure that stores variable and function bindings for a specific scope, along with a reference to its outer environment.

### How does this work internally?
**Answer:** `this` is determined at call time for regular functions based on how the function is invoked. For arrow functions, `this` is captured lexically from the surrounding scope at creation time.

### Explain the Prototype Chain in depth.
**Answer:** Every object can inherit from another object through its internal prototype link. When a property is accessed, JavaScript first checks the object itself, then its prototype, then that prototype's prototype, continuing until it reaches `null`. That lookup sequence is the prototype chain.

### How does garbage collection work?
**Answer:** Garbage collection works by identifying objects that are no longer reachable from the root set, such as global references, active stack references, and closures, and then reclaiming their memory.

### Explain mark-and-sweep garbage collection.
**Answer:** Mark-and-sweep starts from root references, marks every reachable object, and then sweeps through memory to remove everything unmarked. It is one of the core strategies used by modern JavaScript engines.

### What causes memory leaks in JavaScript?
**Answer:** Common causes include accidental global variables, unremoved event listeners, timers that continue running, large closures holding references, detached DOM nodes, and caches that grow without cleanup.

### How do async/await work under the hood?
**Answer:** `async/await` is built on top of promises. An `async` function always returns a promise, and `await` pauses execution of that function until the promise settles, while the rest of JavaScript continues running through the event loop.

### Explain Promise internals.
**Answer:** A promise is an object with an internal state and result. It starts pending, then transitions to fulfilled or rejected exactly once. Handlers registered through `.then`, `.catch`, or `.finally` are queued as microtasks once the promise settles.

### Explain how JavaScript handles concurrency despite being single-threaded.
**Answer:** JavaScript itself runs on one main thread, but concurrency is achieved because the runtime or browser handles async work like timers, network requests, and I/O outside the main stack, and then schedules callbacks through queues and the event loop.

### Explain JIT compilation.
**Answer:** JIT compilation means the engine compiles code during execution. It often starts with quick baseline execution, identifies hot code paths, and then recompiles them into optimized machine code for better performance.

### What is an Abstract Syntax Tree (AST)?
**Answer:** An AST is a tree representation of source code structure created by the parser. Tools like compilers, linters, and bundlers use it to analyze and transform code.

### Explain shallow copy vs deep copy.
**Answer:** A shallow copy copies only the top-level structure, so nested objects still share references. A deep copy recursively copies nested values so the new structure is fully independent.

### Explain reference equality vs value equality.
**Answer:** Value equality means two primitives have the same actual value. Reference equality means two variables point to the exact same object in memory.

### How does module loading work in JavaScript?
**Answer:** When a module is imported, the runtime resolves its path, loads and parses the file, executes it once, and then caches the module so future imports reuse the same instance.

---

## 26. Rapid-Fire Interview Questions

### var vs let vs const
**Answer:** `var` is function-scoped and redeclarable, `let` is block-scoped and reassignable, and `const` is block-scoped but not reassignable.

### null vs undefined
**Answer:** `undefined` means not assigned, while `null` means intentionally empty.

### == vs ===
**Answer:** `==` allows coercion; `===` compares type and value strictly.

### call vs apply vs bind
**Answer:** `call` and `apply` invoke immediately, `bind` returns a new bound function.

### map vs forEach
**Answer:** `map` returns a new array; `forEach` is for side effects.

### map vs filter vs reduce
**Answer:** `map` transforms, `filter` selects, `reduce` accumulates.

### slice vs splice
**Answer:** `slice` does not mutate; `splice` mutates the original array.

### Spread vs Rest
**Answer:** Spread expands values; rest collects values.

### Promise vs async/await
**Answer:** `async/await` is cleaner syntax built on top of promises.

### Object.freeze vs Object.seal
**Answer:** `freeze` prevents all changes; `seal` allows modifying existing properties but not adding or removing them.

### Stack vs Heap
**Answer:** Stack handles execution contexts and simple values; heap stores reference-type objects.

### Primitive vs Reference Types
**Answer:** Primitives are copied by value; reference types are copied by reference.

### Arrow Function vs Normal Function
**Answer:** Arrow functions have lexical `this`; normal functions have dynamic `this`.

### Function Declaration vs Function Expression
**Answer:** Function declarations are fully hoisted; function expressions are not.

### Synchronous vs Asynchronous
**Answer:** Synchronous blocks execution; asynchronous does not block the main flow.

### Event Bubbling vs Capturing
**Answer:** Bubbling goes upward from target; capturing goes downward to target.

### Deep Copy vs Shallow Copy
**Answer:** Shallow copy shares nested references; deep copy duplicates nested structures too.

### Object vs Map
**Answer:** `Object` is good for simple key-value pairs, while `Map` is better for flexible key types and frequent additions or deletions.

### Set vs Array
**Answer:** `Set` stores unique values; `Array` is ordered and allows duplicates.

### Prototype vs Class
**Answer:** Prototype is the actual inheritance mechanism; class is syntactic sugar over it.

### Debounce vs Throttle
**Answer:** Debounce delays until inactivity; throttle limits frequency.

### LocalStorage vs SessionStorage vs Cookies
**Answer:** `localStorage` persists until cleared, `sessionStorage` lasts for the session, and cookies can be sent with HTTP requests and have expiration and security attributes.

### for...in vs for...of
**Answer:** `for...in` iterates over object keys, while `for...of` iterates over iterable values.

### Function Scope vs Block Scope
**Answer:** Function scope belongs to functions, mainly with `var`; block scope belongs to blocks, with `let` and `const`.

### Lexical Scope vs Dynamic Scope
**Answer:** JavaScript uses lexical scope, meaning scope is decided by where code is written, not how it is called.

### Composition vs Inheritance
**Answer:** Composition builds behavior by combining smaller parts, while inheritance builds behavior through parent-child hierarchies. In JavaScript, composition is usually preferred for flexibility.
