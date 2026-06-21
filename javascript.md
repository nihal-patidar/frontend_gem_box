# 02_JavaScript_Core.md

# JavaScript Core Revision Sheet

Purpose:

This document contains the most important JavaScript concepts, syntax, patterns, and common mistakes required for React and MERN projects.

---

# Table of Contents

1. Variables
2. Data Types
3. Operators
4. Functions
5. Arrow Functions
6. Template Literals
7. Destructuring
8. Spread Operator
9. Rest Operator
10. Arrays
11. Objects
12. Array Methods
13. Object Methods
14. Conditional Rendering
15. Short Circuiting
16. Optional Chaining
17. Nullish Coalescing
18. Async JavaScript
19. Fetch API
20. Common React Patterns
21. Common Mistakes
22. Copy-Paste Snippets

---

# 1. Variables

## let

```js
let age = 21;
age = 22;
```

Can be reassigned.

---

## const

```js
const name = "Nihal";
```

Cannot be reassigned.

---

## var

```js
var city = "Indore";
```

Avoid using var.

---

# 2. Data Types

## Primitive

```js
String
Number
Boolean
Undefined
Null
BigInt
Symbol
```

Example:

```js
const name = "Nihal";
const age = 21;
const isPlaced = true;
const data = null;
```

---

## Non Primitive

```js
Object
Array
Function
```

Example:

```js
const user = {};
const users = [];
const greet = () => {};
```

---

# 3. Operators

## Comparison

```js
==
===
!=
!==
>
<
>=
<=
```

Always prefer:

```js
===
!==
```

---

## Logical

```js
&&
||
!
```

Example:

```js
if (isLoggedIn && isVerified) {
}
```

---

# 4. Functions

## Normal Function

```js
function greet() {
  console.log("Hello");
}
```

---

## Function With Parameters

```js
function greet(name) {
  console.log(name);
}
```

---

## Return Value

```js
function add(a, b) {
  return a + b;
}
```

---

# 5. Arrow Functions

```js
const greet = () => {
  console.log("Hello");
};
```

---

## Single Line Return

```js
const add = (a, b) => a + b;
```

---

# 6. Template Literals

```js
const name = "Nihal";

console.log(`Hello ${name}`);
```

---

# 7. Destructuring

## Object

```js
const user = {
  name: "Nihal",
  age: 21,
};

const { name, age } = user;
```

---

## Array

```js
const colors = ["red", "blue"];

const [first, second] = colors;
```

---

# 8. Spread Operator

## Array Copy

```js
const arr = [1, 2];

const newArr = [...arr];
```

---

## Object Copy

```js
const user = {
  name: "Nihal",
};

const newUser = {
  ...user,
};
```

---

## Add New Property

```js
const updatedUser = {
  ...user,
  city: "Indore",
};
```

---

# 9. Rest Operator

```js
function sum(...numbers) {
  console.log(numbers);
}
```

# 🎭 Bonus: JavaScript Truthy, Falsy, and Abstract Equality Reference

Understanding JavaScript's type coercion and quirky comparison rules prevents critical runtime routing or conditional bugs. Keep this reference handy for complex feature logic.

---

## 1. Truthy vs. Falsy Cheat Sheet

In JavaScript, a value is **falsy** if it translates to `false` when evaluated in a boolean context (like an `if` condition). **Everything else is truthy.**

### The 8 Falsy Values
* `false` (The boolean itself)
* `0`, `-0`, `0n` (Zero numbers, including BigInt zero)
* `""`, `''`, ``` (Empty strings)
* `null` (Absence of any value)
* `undefined` (Uninitialized value)
* `NaN` (Not a Number)

### Commonly Mistaken "Truthy" Values
* `[]` (Empty arrays are **truthy**)
* `{}` (Empty objects are **truthy**)
* `" "` (A string with just a space is **truthy**)
* `"false"` (The string text `"false"` is **truthy**)

---

## 2. Array and `null`/`0` Comparison Breakdown

When comparing arrays using abstract equality (`==`) or strict equality (`===`), JavaScript evaluates them by **reference memory pointer**, not by content value. 

Here is exactly how the engine computes the tricky comparisons:

| Comparison | Result | Why It Happens |
| :--- | :--- | :--- |
| `[] == null` | **`false`** | `null` only loosely equals (`==`) `null` or `undefined`. It does not coerce to match objects or arrays. |
| `[] === null` | **`false`** | Strict equality check fails immediately because types differ (`object` vs `object/null`). |
| `[] == 0` | **`true`** | **The trap!** JavaScript converts the array to a primitive string (`[].toString()` becomes `""`). An empty string `""` coerced to a number becomes `0`. Therefore, `0 == 0`. |
| `[] === 0` | **`false`** | Strict equality check fails instantly due to different types (`object` vs `number`). |
| `[] == ![]` | **`true`** | `![]` evaluates to `false` (since `[]` is truthy). This leaves `[] == false`. JavaScript coerces both to numbers: `[]` becomes `0`, and `false` becomes `0`. `0 == 0` evaluates to true. |
| `[] == []` | **`false`** | Both are unique instances in memory. Two distinct object pointers are never equal to each other. |

---

## 3. Best Practices for Features
* **Always use `===` (Strict Equality):** This completely bypasses implicit type coercion traps like `[] == 0`.
* **Explicit Array Checking:** To check if an array actually contains elements, don't rely on implicit booleans. Always check length explicitly: 
  ```javascript
  if (myArray.length > 0) { ... }
  ```
```

---

# 10. Arrays

## Create Array

```js
const users = [];
```

---

## Add Item

```js
users.push("Nihal");
```

---

## Remove Last Item

```js
users.pop();
```

---

## Remove First Item

```js
users.shift();
```

---

## Add First Item

```js
users.unshift("Nihal");
```

---

# 11. Objects

## Create Object

```js
const user = {
  name: "Nihal",
  age: 21,
};
```

---

## Access

```js
user.name

user["name"]
```

---

## Update

```js
user.age = 22;
```

---

## Add

```js
user.city = "Indore";
```

---

## Delete

```js
delete user.city;
```

---

# 12. Array Methods

# map()

Transforms array.

```js
const nums = [1, 2, 3];

const result = nums.map((num) => num * 2);
```

Result:

```js
[2, 4, 6]
```

---

### Common Mistake

Wrong:

```js
nums.map((num) => {
  num * 2;
});
```

No return.

---

Correct:

```js
nums.map((num) => {
  return num * 2;
});
```

---

# filter()

Returns matching elements.

```js
const users = [
  { age: 18 },
  { age: 25 },
];

const adults = users.filter(
  (user) => user.age >= 18
);
```

---

### Common Mistake

Wrong:

```js
users.filter(
  (user) => user.age = 18
);
```

Assignment operator.

---

Correct:

```js
users.filter(
  (user) => user.age === 18
);
```

---

# find()

Returns first matching element.

```js
const user = users.find(
  (user) => user.id === 1
);
```

---

Difference:

```js
find() → Object

filter() → Array
```

---

# findIndex()

```js
const index = users.findIndex(
  (user) => user.id === 1
);
```

---

# some()

Returns boolean.

```js
const exists = users.some(
  (user) => user.id === 1
);
```

---

# every()

```js
const valid = users.every(
  (user) => user.age >= 18
);
```

---

# reduce()

```js
const nums = [1, 2, 3];

const total = nums.reduce(
  (acc, curr) => acc + curr,
  0
);
```

---

# sort()

```js
const nums = [5, 1, 3];

nums.sort((a, b) => a - b);
```

Ascending.

---

# 13. Object Update Patterns

## Update Property

```js
const updatedUser = {
  ...user,
  age: 22,
};
```

---

## Nested Update

```js
const updatedUser = {
  ...user,
  address: {
    ...user.address,
    city: "Indore",
  },
};
```

## Dynamic Key Update
```js
const updatedUser = {
  ...user,
  [keyToUpdate]: newValue // Computed property name
};
```


## Expression as value in Object 

```js
const userStatus = {
  // 1. Math expression
  age: 20 + 6, 
  
  // 2. Ternary operator expression
  canVote: user.age >= 18 ? true : false, 
  
  // 3. Function call expression
  lastLogin: Date.now(), 
  
  // 4. Logical OR expression (Logical assignment)
  theme: localStorage.getItem("theme") || "dark" 
};
```

## Immediate Function Executions (IIFE): 
If you absolutely need complex logic or loops inside the object, wrap it in a self-executing function that returns a value.javascript
```js
const user = {
  idList: (() => {
    let arr = [];
    for(let i = 0; i < 3; i++) arr.push(i);
    return arr; // Returns [0, 1, 2]
  })()
};
```

---

# 14. Conditional Rendering

## if

```js
if (isLoggedIn) {
}
```

---

## Ternary

```js
isLoggedIn
  ? "Welcome"
  : "Login";
```

---

# 15. Short Circuit

```js
isLoggedIn && <Dashboard />
```

---

# 16. Optional Chaining

Avoid crashes.

Wrong:

```js
user.address.city
```

---

Correct:

```js
user?.address?.city
```

---

# 17. Nullish Coalescing

```js
const name = userName ?? "Guest";
```

---

# 18. Async JavaScript

## Promise

```js
fetch(url)
  .then()
  .catch();
```

---

## Async Await

```js
async function getData() {
}
```

---

# 19. Fetch API

## GET Request

```js
const response = await fetch(url);

const data = await response.json();
```

---

## Full Pattern

```js
try {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error("Failed");
  }

  const data = await response.json();

} catch (error) {

  console.log(error);

} finally {

}
```

---

# 20. React Useful Patterns

## Render List

```jsx
products.map((product) => (
  <ProductItem
    key={product.id}
    product={product}
  />
));
```

---

## Conditional Rendering

```jsx
if (loading)
  return <Loader />;
```

---

## Error Rendering

```jsx
if (error)
  return (
    <ErrorMessage
      message={error}
    />
  );
```

---

# 21. Common Mistakes

## map Without Return

Wrong:

```js
arr.map((item) => {
  item;
});
```

---

## filter Used As Delete

Wrong:

```js
arr.filter(
  (item) => item.id !== id
);
```

Forgot assignment.

---

Correct:

```js
arr = arr.filter(
  (item) => item.id !== id
);
```

---

## find Returns Object

Wrong:

```js
find().map()
```

---

## Optional Chaining Missing

Wrong:

```js
user.address.city
```

---

Correct:

```js
user?.address?.city
```

---

## State Mutation

Wrong:

```js
state.items.push(item);
```

Outside Redux.

---

Correct:

```js
setItems([
  ...items,
  item,
]);
```

---

# 22. Copy-Paste Snippets

## Add Item

```js
const newItems = [
  ...items,
  item,
];
```

---

## Remove Item

```js
const updatedItems =
  items.filter(
    (item) =>
      item.id !== id
  );
```

---

## Update Item

```js
const updatedItems =
  items.map((item) =>
    item.id === id
      ? {
          ...item,
          qty: item.qty + 1,
        }
      : item
  );
```

---

## Find Item

```js
const product =
  products.find(
    (item) => item.id === id
  );
```

---

## Check Exists

```js
const exists =
  items.some(
    (item) => item.id === id
  );
```

---

# Golden Rules

1. Prefer const.
2. Use === instead of ==.
3. Use map for rendering.
4. Use filter for deleting.
5. Use find for single item.
6. Never mutate state directly.
7. Use optional chaining.
8. Always handle API errors.
9. Use async/await over nested .then().
10. Read error messages carefully before debugging.