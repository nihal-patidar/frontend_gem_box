# 04_React_Hooks.md

# React Hooks Master Revision Sheet

Purpose:

This document contains everything required to understand, revise, and use React Hooks efficiently in real-world projects.

This file should remove the need to repeatedly search hook syntax.

---

# Table of Contents

1. What Are Hooks
2. Rules of Hooks
3. useState
4. useEffect
5. useRef
6. useContext
7. useMemo
8. useCallback
9. Custom Hooks
10. Hook Decision Guide
11. Common Patterns
12. Common Mistakes
13. Interview Notes
14. Copy-Paste Templates

---

# 1. What Are Hooks

Hooks allow functional components to use React features such as:

```txt
State
Lifecycle
Context
Performance Optimization
DOM Access
```

Before Hooks:

```txt
Class Components
```

After Hooks:

```txt
Functional Components
```

---

# 2. Rules of Hooks

## Rule 1

Always call Hooks at the top level.

Wrong:

```jsx
if (isLoggedIn) {
  useState();
}
```

---

Correct:

```jsx
const [user, setUser] =
  useState(null);
```

---

## Rule 2

Only call Hooks:

```txt
React Components
Custom Hooks
```

Wrong:

```js
function helper() {
  useState();
}
```

---

Correct:

```js
function Component() {
  useState();
}
```

---

# 3. useState

Purpose:

```txt
Manage Component State
```

Import:

```jsx
import { useState } from "react";
```

---

Basic Syntax

```jsx
const [count, setCount] =
  useState(0);
```

---

Reading State

```jsx
count
```

---

Updating State

```jsx
setCount(1);
```

---

Increment

```jsx
setCount(count + 1);
```

---

Preferred Increment

```jsx
setCount(prev => prev + 1);
```

---

String State

```jsx
const [name, setName] =
  useState("");
```

---

Array State

```jsx
const [items, setItems] =
  useState([]);
```

---

Object State

```jsx
const [user, setUser] =
  useState({});
```

---

Update Object

```jsx
setUser({
  ...user,
  age: 22,
});
```

---

# 4. useEffect

Purpose:

```txt
Side Effects
```

Examples:

```txt
API Calls
Timers
Subscriptions
DOM Operations
```

---

Import

```jsx
import { useEffect } from "react";
```

---

Run Once

```jsx
useEffect(() => {

}, []);
```

Equivalent:

```txt
Component Did Mount
```

---

Run On State Change

```jsx
useEffect(() => {

}, [search]);
```

Runs when:

```txt
search changes
```

---

Run Every Render

```jsx
useEffect(() => {

});
```

Avoid unless necessary.

---

Cleanup Function

```jsx
useEffect(() => {

  return () => {

  };

}, []);
```

Equivalent:

```txt
Component Unmount
```

---

API Call Pattern

```jsx
useEffect(() => {

  async function fetchData() {

    try {

    } catch (error) {

    }

  }

  fetchData();

}, []);
```

---

Never Do This

Wrong:

```jsx
useEffect(async () => {

}, []);
```

Reason:

```txt
useEffect expects cleanup function
not Promise
```

---

# 5. useRef

Purpose:

```txt
Access DOM
Store Value Without Re-render
```

Import

```jsx
import { useRef } from "react";
```

---

Create Ref

```jsx
const inputRef = useRef();
```

---

Attach

```jsx
<input ref={inputRef} />
```

---

Focus Input

```jsx
inputRef.current.focus();
```

---

Store Previous Value

```jsx
const prevValue =
  useRef();
```

---

Difference

useState

```txt
Re-renders Component
```

useRef

```txt
Does Not Re-render
```

---

# 6. useContext

Purpose:

```txt
Global State Without Prop Drilling
```

---

Create Context

```jsx
import {
  createContext
} from "react";

export const UserContext =
  createContext();
```

---

Provider

```jsx
<UserContext.Provider
  value={user}
>
  <App />
</UserContext.Provider>
```

---

Consume

```jsx
const user =
  useContext(UserContext);
```

---

Use When

```txt
Theme
Language
Authentication
User Data
```

---

Avoid For

```txt
Complex State
Large Applications
```

Use Redux instead.

---

# 7. useMemo

Purpose:

```txt
Memoize Expensive Calculations
```

Import

```jsx
import { useMemo } from "react";
```

---

Syntax

```jsx
const filteredProducts =
  useMemo(() => {

    return products.filter(
      product =>
      product.price > 100
    );

  }, [products]);
```

---

Without useMemo

```txt
Calculation Runs Every Render
```

---

With useMemo

```txt
Calculation Runs Only When Dependency Changes
```

---

Use Cases

```txt
Filtering
Sorting
Large Lists
Heavy Computations
```

---

# 8. useCallback

Purpose:

```txt
Memoize Functions
```

Import

```jsx
import {
  useCallback
} from "react";
```

---

Syntax

```jsx
const handleDelete =
  useCallback(() => {

  }, []);
```

---

Use Cases

```txt
Passing Functions To Children
Prevent Re-renders
```

---

# 9. Custom Hooks

Purpose:

```txt
Reuse Logic
```

---

Naming Rule

Must Start With:

```txt
use
```

Examples:

```txt
useProducts
useAuth
useTheme
```

---

Example

```jsx
function useProducts() {

  const [products,
    setProducts] =
      useState([]);

  return products;
}
```

---

Usage

```jsx
const products =
  useProducts();
```

---

# 10. Hook Decision Guide

Need State?

```txt
useState
```

---

Need API Call?

```txt
useEffect
```

---

Need DOM Access?

```txt
useRef
```

---

Need Global Data?

```txt
useContext
Redux
```

---

Need Reusable Logic?

```txt
Custom Hook
```

---

Need Performance Optimization?

```txt
useMemo
useCallback
```

---

# 11. Common Patterns

Loader

```jsx
if (loading)
  return <Loader />;
```

---

Error

```jsx
if (error)
  return (
    <ErrorMessage
      message={error}
    />
  );
```

---

Fetch Products

```jsx
const {
  products,
  loading,
  error
} = useProducts();
```

---

Input Focus

```jsx
inputRef.current.focus();
```

---

# 12. Common Mistakes

## Missing Dependency

Wrong

```jsx
useEffect(() => {

}, []);
```

while using:

```jsx
search
```

inside effect.

---

## Infinite Loop

Wrong

```jsx
useEffect(() => {

  setCount(count + 1);

}, [count]);
```

---

## Direct State Mutation

Wrong

```jsx
user.age = 22;
```

---

Correct

```jsx
setUser({
  ...user,
  age: 22,
});
```

---

## useRef Expecting Re-render

Wrong

```txt
Updating ref and expecting UI update
```

---

## useEffect Async Directly

Wrong

```jsx
useEffect(async () => {

}, []);
```

---

# 13. Interview Notes

## useState

```txt
Manages State
Triggers Re-render
```

---

## useEffect

```txt
Handles Side Effects
```

---

## useRef

```txt
Stores Mutable Values
Access DOM
No Re-render
```

---

## useContext

```txt
Avoid Prop Drilling
```

---

## useMemo

```txt
Memoizes Values
```

---

## useCallback

```txt
Memoizes Functions
```

---

## Custom Hook

```txt
Reusable Logic
```

---

# 14. Copy-Paste Templates

## useState

```jsx
const [value, setValue] =
  useState("");
```

---

## useEffect

```jsx
useEffect(() => {

}, []);
```

---

## API Fetch

```jsx
useEffect(() => {

  async function getData() {

    try {

      const response =
        await fetch(url);

      const data =
        await response.json();

    } catch (error) {

      console.log(error);

    }

  }

  getData();

}, []);
```

---

## useRef

```jsx
const inputRef =
  useRef();
```

---

## useMemo

```jsx
const result =
  useMemo(() => {

    return value;

  }, [value]);
```

---

## useCallback

```jsx
const handleClick =
  useCallback(() => {

  }, []);
```

---

## Custom Hook

```jsx
function useCustom() {

  const [data, setData] =
    useState([]);

  return data;
}
```

---

# Golden Rules

1. Never Call Hooks Inside Conditions.
2. Never Call Hooks Inside Loops.
3. Prefer useState For Local State.
4. Use useEffect For API Calls.
5. Use useRef For DOM Access.
6. Create Custom Hooks For Reusable Logic.
7. Don't Overuse useMemo.
8. Don't Overuse useCallback.
9. Keep Effects Small.
10. Read Dependency Arrays Carefully.