# 03_React_Core.md

# React Core Revision Sheet

Purpose:

This document contains everything required to build React applications confidently after a long gap.

Keep this file open whenever starting a React project.

---

# Table of Contents

1. What is React
2. Why React
3. React Project Structure
4. JSX Fundamentals
5. Components
6. Functional Components
7. Props
8. Children Props
9. State
10. Event Handling
11. Conditional Rendering
12. Lists and Keys
13. Forms
14. Controlled Components
15. Lifting State Up
16. Component Communication
17. Reusable Components
18. React Fragment
19. React.StrictMode
20. Component Lifecycle
21. Common React Patterns
22. Common Mistakes
23. Copy-Paste Templates
24. Project Checklist

---

# 1. What is React

React is a JavaScript library used to build User Interfaces.

Created by:

```txt
Meta (Facebook)
```

React follows:

```txt
Component Based Architecture
```

---

# 2. Why React

Without React:

```txt
HTML
CSS
JavaScript
DOM Manipulation
```

Problems:

```txt
Difficult State Management
Code Repetition
Poor Scalability
```

React solves:

```txt
Reusable Components
State Management
Virtual DOM
Better Performance
```

---

# 3. React Project Structure

Recommended:

```txt
src/
│
├── app/
├── redux/
├── hooks/
├── routes/
├── pages/
├── components/
├── utils/
├── services/
├── assets/
├── styles/
│
├── App.jsx
└── main.jsx
```

---

# 4. JSX Fundamentals

JSX = JavaScript XML

Allows writing HTML inside JavaScript.

Example:

```jsx
function App() {
  return <h1>Hello React</h1>;
}
```

---

# JSX Rules

## Must Return Single Parent

Wrong:

```jsx
return (
  <h1>Hello</h1>
  <p>World</p>
)
```

---

Correct:

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
)
```

---

## Use className

Wrong:

```jsx
<div class="card"></div>
```

Correct:

```jsx
<div className="card"></div>
```

---

## Use htmlFor

Wrong:

```jsx
<label for="name"></label>
```

Correct:

```jsx
<label htmlFor="name"></label>
```

---

# 5. Components

Component:

```txt
Reusable UI Block
```

Examples:

```txt
Header
Navbar
Sidebar
ProductCard
Footer
```

---

# Component Naming Rule

Always:

```txt
PascalCase
```

Correct:

```jsx
ProductCard
UserProfile
```

Wrong:

```jsx
productCard
userProfile
```

---

# 6. Functional Components

Standard Component:

```jsx
function Header() {
  return (
    <h1>Header</h1>
  );
}

export default Header;
```

---

Arrow Function:

```jsx
const Header = () => {
  return (
    <h1>Header</h1>
  );
};

export default Header;
```

---

# 7. Props

Props:

```txt
Parent → Child Communication
```

---

Parent:

```jsx
<ProductCard
  title="Laptop"
/>
```

---

Child:

```jsx
function ProductCard(props) {
  return (
    <h1>{props.title}</h1>
  );
}
```

---

Destructuring Props

Preferred:

```jsx
function ProductCard({
  title,
}) {
  return (
    <h1>{title}</h1>
  );
}
```

---

# 8. Children Props

Parent:

```jsx
<Card>
  Hello World
</Card>
```

---

Child:

```jsx
function Card({
  children,
}) {
  return (
    <div>
      {children}
    </div>
  );
}
```

---

# 9. State

State:

```txt
Dynamic Data
```

Example:

```jsx
const [count, setCount] =
  useState(0);
```

---

Access State

```jsx
count
```

---

Update State

```jsx
setCount(1);
```

---

# 10. Event Handling

Button Click:

```jsx
<button
  onClick={handleClick}
>
  Click
</button>
```

---

Function:

```jsx
function handleClick() {
  console.log("Clicked");
}
```

---

Inline:

```jsx
<button
  onClick={() =>
    console.log("Click")
  }
>
```

---

# 11. Conditional Rendering

## if Statement

```jsx
if (loading) {
  return <Loader />;
}
```

---

## Ternary

```jsx
{
  loading
    ? <Loader />
    : <ProductList />
}
```

---

## AND Operator

```jsx
{
  loading &&
  <Loader />
}
```

---

# 12. Lists and Keys

Render List:

```jsx
products.map((product) => (
  <ProductCard
    key={product.id}
    product={product}
  />
));
```

---

# Key Rule

Wrong:

```jsx
key={index}
```

Avoid when possible.

---

Preferred:

```jsx
key={product.id}
```

---

# 13. Forms

Basic Input:

```jsx
<input
  type="text"
/>
```

---

# 14. Controlled Components

State Controlled Input

```jsx
const [name, setName] =
  useState("");
```

---

```jsx
<input
  value={name}
  onChange={(e) =>
    setName(e.target.value)
  }
/>
```

---

# 15. Lifting State Up

Problem:

```txt
Sibling Components Need Same Data
```

Move state to parent.

---

Wrong:

```txt
Child A Own State
Child B Own State
```

---

Correct:

```txt
Parent Own State

↓ Pass Props

Child A
Child B
```

---

# 16. Component Communication

Parent → Child

```txt
Props
```

---

Child → Parent

```txt
Callback Function
```

---

Example:

Parent:

```jsx
<Child
  onDelete={handleDelete}
/>
```

---

Child:

```jsx
<button
  onClick={() =>
    onDelete(id)
  }
>
```

---

# 17. Reusable Components

Bad:

```jsx
ProductCard1
ProductCard2
ProductCard3
```

---

Good:

```jsx
<ProductCard
  product={product}
/>
```

---

# 18. React Fragment

Avoid Extra Divs.

Wrong:

```jsx
<div>
  <h1 />
  <p />
</div>
```

---

Preferred:

```jsx
<>
  <h1 />
  <p />
</>
```

---

# 19. React.StrictMode

Location:

```jsx
main.jsx
```

---

Purpose:

```txt
Detect Problems
Highlight Unsafe Code
```

---

Example:

```jsx
<StrictMode>
  <App />
</StrictMode>
```

---

# 20. Component Lifecycle

Mount

```txt
Component Created
```

---

Update

```txt
State Changed
Props Changed
```

---

Unmount

```txt
Component Removed
```

---

React Handles Lifecycle Through:

```txt
useEffect
```

---

# 21. Common React Patterns

Loader Pattern

```jsx
if (loading)
  return <Loader />;
```

---

Error Pattern

```jsx
if (error)
  return (
    <ErrorMessage
      message={error}
    />
  );
```

---

No Data Pattern

```jsx
if (!products.length)
  return (
    <p>No Products</p>
  );
```

---

# 22. Common Mistakes

## Forgot Return

Wrong:

```jsx
const App = () => {
  <h1>Hello</h1>;
};
```

---

Correct:

```jsx
const App = () => {
  return <h1>Hello</h1>;
};
```

---

## Missing Key

Wrong:

```jsx
items.map(item => (
  <Card />
))
```

---

Correct:

```jsx
items.map(item => (
  <Card
    key={item.id}
  />
))
```

---

## Calling Function Immediately

Wrong:

```jsx
onClick={handleDelete()}
```

---

Correct:

```jsx
onClick={handleDelete}
```

---

## Updating State Directly

Wrong:

```jsx
count = count + 1;
```

---

Correct:

```jsx
setCount(count + 1);
```

---

## Using Class Instead Of className

Wrong:

```jsx
<div class="box">
```

---

Correct:

```jsx
<div className="box">
```

---

# 23. Copy-Paste Templates

Component Template

```jsx
function Component() {
  return (
    <div>
      Component
    </div>
  );
}

export default Component;
```

---

Props Template

```jsx
function Card({
  title,
}) {
  return (
    <h1>{title}</h1>
  );
}

export default Card;
```

---

State Template

```jsx
const [value, setValue] =
  useState("");
```

---

Input Template

```jsx
<input
  value={value}
  onChange={(e) =>
    setValue(
      e.target.value
    )
  }
/>
```

---

Map Template

```jsx
items.map((item) => (
  <Card
    key={item.id}
    item={item}
  />
));
```

---

# 24. Project Checklist

Before Building:

```txt
□ Folder Structure Ready

□ Components Planned

□ Routing Planned

□ State Strategy Planned

□ API Structure Planned
```

Before Submission:

```txt
□ No Console Errors

□ Responsive Design

□ Proper Keys

□ Proper Props

□ Reusable Components

□ Error Handling

□ Loading State

□ Clean Code
```

---

# Golden Rules

1. Components Must Be Reusable.
2. Props Flow Parent → Child.
3. State Should Live At Proper Level.
4. Never Mutate State Directly.
5. Always Use Keys In Lists.
6. Prefer Small Components.
7. Keep Logic Separate From UI.
8. Use Conditional Rendering Properly.
9. Reuse Components.
10. Think In Components, Not Pages.