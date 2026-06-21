# 06_Redux_Toolkit.md

# Redux Toolkit Master Revision Sheet

Purpose:

This document contains everything required to setup, understand, debug, and use Redux Toolkit in React applications.

Use this file whenever starting a Redux project.

---

# Table of Contents

1. What is Redux
2. Why Redux
3. Redux Data Flow
4. Installation
5. Folder Structure
6. Store Setup
7. createSlice
8. Reducers
9. Actions
10. Provider
11. useSelector
12. useDispatch
13. State Structure
14. Cart Implementation
15. Search Implementation
16. CRUD Patterns
17. Common Mistakes
18. Debugging Guide
19. Interview Notes
20. Copy-Paste Templates
21. Project Checklist

---

# 1. What is Redux

Redux is a global state management library.

Without Redux:

```txt
Props Drilling
Parent → Child → Child → Child
```

With Redux:

```txt
Global Store
```

Any component can access data directly.

---

# 2. Why Redux

Use Redux When:

```txt
Cart State
Authentication
Theme
User Data
Search State
Wishlist
```

Avoid Redux For:

```txt
Simple Input State
Modal Open State
Temporary UI State
```

Use:

```txt
useState
```

instead.

---

# 3. Redux Data Flow

```txt
Component

↓

Dispatch Action

↓

Reducer

↓

Store Updated

↓

Component Re-renders
```

Example:

```txt
Add To Cart

↓

dispatch(addToCart())

↓

cartSlice Reducer

↓

Store Updated

↓

Cart UI Updates
```

---

# 4. Installation

Install Redux Toolkit:

```bash
npm install @reduxjs/toolkit react-redux
```

---

Packages:

```txt
@reduxjs/toolkit
react-redux
```

---

# 5. Folder Structure

```txt
src/

app/
│
└── store.js

redux/
│
├── cartSlice.js
├── searchSlice.js
└── userSlice.js
```

---

# 6. Store Setup

File:

```txt
app/store.js
```

---

Example:

```js
import {
 configureStore
}
from "@reduxjs/toolkit";

import cartReducer
from "../redux/cartSlice";

import searchReducer
from "../redux/searchSlice";

const store =
configureStore({
 reducer: {
  cart: cartReducer,
  search: searchReducer,
 }
});

export default store;
```

---

# 7. createSlice

Purpose:

```txt
Creates

State
Reducers
Actions
```

Automatically.

---

Example:

```js
import {
 createSlice
}
from "@reduxjs/toolkit";

const cartSlice =
createSlice({

 name: "cart",

 initialState: {
  items: []
 },

 reducers: {

 }

});
```

---

# 8. Reducers

Reducer:

```txt
Updates State
```

---

Example:

```js
addToCart:
(state, action) => {

}
```

---

Action Payload

```js
action.payload
```

contains data sent by dispatch.

---

# 9. Actions

Generated Automatically.

---

Example:

```js
export const {
 addToCart
}
=
cartSlice.actions;
```

---

Usage:

```js
dispatch(
 addToCart(product)
);
```

---

# 10. Provider

Purpose:

```txt
Makes Store Available
```

---

Import:

```jsx
import {
 Provider
}
from "react-redux";
```

---

main.jsx

```jsx
<Provider
 store={store}
>

 <Router />

</Provider>
```

---

Without Provider

Error:

```txt
Could not find react-redux context value
```

---

# 11. useSelector

Purpose:

```txt
Read Redux State
```

---

Import:

```jsx
import {
 useSelector
}
from "react-redux";
```

---

Example:

```jsx
const items =
useSelector(
 state =>
 state.cart.items
);
```

---

State Shape

```js
{
 cart: {
  items: []
 }
}
```

---

# 12. useDispatch

Purpose:

```txt
Send Action
```

---

Import:

```jsx
import {
 useDispatch
}
from "react-redux";
```

---

Example:

```jsx
const dispatch =
useDispatch();
```

---

Dispatch Action

```jsx
dispatch(
 addToCart(product)
);
```

---

# 13. State Structure

ShoppyGlobe Example

```js
{
 cart: {
  items: []
 },

 search: {
  item: ""
 }
}
```

---

Access Cart

```jsx
state.cart.items
```

---

Access Search

```jsx
state.search.item
```

---

# 14. Cart Implementation

Add Product

```js
addToCart:
(state, action) => {

 state.items.push(
  action.payload
 );

}
```

---

Remove Product

```js
removeFromCart:
(state, action) => {

 state.items =
 state.items.filter(
  item =>
   item.id !==
   action.payload.id
 );

}
```

---

# Real Cart Pattern

Instead Of:

```txt
Duplicate Products
```

Store:

```js
{
 id: 1,
 title: "Laptop",
 qty: 2
}
```

---

# Increase Quantity

```js
increaseQty:
(state, action) => {

 const item =
 state.items.find(
  item =>
   item.id ===
   action.payload
 );

 if(item){

  item.qty += 1;

 }

}
```

---

# Decrease Quantity

```js
decreaseQty:
(state, action) => {

 const item =
 state.items.find(
  item =>
   item.id ===
   action.payload
 );

 if(
  item &&
  item.qty > 1
 ){

  item.qty -= 1;

 }

}
```

---

# Clear Cart

```js
clearCart:
(state) => {

 state.items = [];

}
```

---

# 15. Search Implementation

Slice:

```js
initialState: {
 item: ""
}
```

---

Reducer:

```js
setSearchItem:
(state, action) => {

 state.item =
 action.payload;

}
```

---

Dispatch:

```jsx
dispatch(
 setSearchItem(
  e.target.value
 )
);
```

---

Read:

```jsx
const searchItem =
useSelector(
 state =>
 state.search.item
);
```

---

# 16. CRUD Patterns

Add

```js
state.items.push(
 action.payload
);
```

---

Read

```js
state.items
```

---

Update

```js
const item =
state.items.find(
 item =>
 item.id === id
);

item.qty += 1;
```

---

Delete

```js
state.items =
state.items.filter(
 item =>
 item.id !== id
);
```

---

# 17. Common Mistakes

## state.cart.items Inside Slice

Wrong

```js
state.cart.items
```

---

Correct

```js
state.items
```

Reason:

Inside reducer:

```txt
state already points
to slice state
```

---

## Forgot Reducer Export

Wrong

```js
export default cartSlice;
```

---

Correct

```js
export default
cartSlice.reducer;
```

---

## Forgot Actions Export

Wrong

```js
No Action Export
```

---

Correct

```js
export const {
 addToCart
}
=
cartSlice.actions;
```

---

## Forgot Provider

Error:

```txt
Could not find
react-redux context value
```

---

## Wrong State Path

Wrong

```js
state.items
```

from component.

---

Correct

```js
state.cart.items
```

---

# 18. Debugging Guide

Problem:

```txt
Dispatch Not Working
```

Check:

```txt
Provider
Store
Dispatch
```

---

Problem:

```txt
Selector Undefined
```

Check:

```txt
State Path
Store Setup
```

---

Problem:

```txt
Reducer Not Running
```

Check:

```txt
Action Export
Reducer Export
Store Reducer
```

---

Problem:

```txt
Cart Not Updating
```

Check:

```txt
Payload
ID Matching
```

---

# 19. Interview Notes

Redux

```txt
Global State Management
```

---

Store

```txt
Single Source Of Truth
```

---

Reducer

```txt
Updates State
```

---

Action

```txt
Describes Change
```

---

useSelector

```txt
Read State
```

---

useDispatch

```txt
Send Action
```

---

Redux Toolkit

```txt
Official Redux Tool
Reduces Boilerplate
```

---

# 20. Copy-Paste Templates

Store

```js
const store =
configureStore({
 reducer: {

 }
});
```

---

Slice

```js
const slice =
createSlice({

 name: "",

 initialState: {},

 reducers: {

 }

});
```

---

Selector

```jsx
const data =
useSelector(
 state =>
 state.cart.items
);
```

---

Dispatch

```jsx
const dispatch =
useDispatch();

dispatch(
 action(payload)
);
```

---

Provider

```jsx
<Provider
 store={store}
>

 <App />

</Provider>
```

---

# 21. Project Checklist

Before Redux:

```txt
□ Install Redux Toolkit

□ Create Store

□ Create Slice

□ Export Actions

□ Export Reducer
```

---

Before Using Redux:

```txt
□ Wrap Provider

□ Configure Store

□ Verify State Shape

□ Test Dispatch

□ Test Selector
```

---

Before Submission:

```txt
□ Cart Works

□ Search Works

□ Quantity Works

□ Remove Works

□ Clear Cart Works

□ No Console Errors
```

---

# Golden Rules

1. Use Redux For Global State.
2. Use useState For Local State.
3. Always Export Reducer.
4. Always Export Actions.
5. Provider Must Wrap App.
6. Read State Using useSelector.
7. Update State Using Dispatch.
8. Keep State Minimal.
9. Don't Store Unnecessary Data.
10. Learn State Shape First Before Debugging.