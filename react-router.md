# 05_React_Router.md

# React Router DOM Master Revision Sheet

Purpose:

This document contains everything required to setup, understand, debug, and use React Router in modern React applications.

Use this file whenever starting a React project.

---

# Table of Contents

1. What is React Router
2. Installation
3. Router Architecture
4. createBrowserRouter
5. RouterProvider
6. Layout Routes
7. Outlet
8. Link
9. NavLink
10. Route Parameters
11. useParams
12. useNavigate
13. useLocation
14. Dynamic Routes
15. Nested Routes
16. Not Found Route
17. Protected Routes
18. Common Folder Structure
19. Common Mistakes
20. Debugging Guide
21. Interview Notes
22. Copy-Paste Templates
23. Project Checklist

---

# 1. What is React Router

React Router allows navigation between pages without reloading the browser.

Without Router:

```txt
Traditional Multi Page Application
```

With Router:

```txt
Single Page Application (SPA)
```

---

# 2. Installation

Install:

```bash
npm install react-router-dom
```

Verify:

```json
"react-router-dom"
```

exists in:

```txt
package.json
```

---

# 3. Router Architecture

Typical Flow:

```txt
main.jsx
    ↓
RouterProvider
    ↓
Router Configuration
    ↓
Layout
    ↓
Outlet
    ↓
Pages
```

---

# 4. createBrowserRouter

Modern Router API.

Import:

```jsx
import {
  createBrowserRouter
} from "react-router-dom";
```

---

Basic Example:

```jsx
const router =
  createBrowserRouter([
    {
      path: "/",
      element: <Home />
    }
  ]);
```

---

# 5. RouterProvider

Purpose:

```txt
Provides Router To Entire App
```

Import:

```jsx
import {
  RouterProvider
} from "react-router-dom";
```

---

Example:

```jsx
<RouterProvider
  router={router}
/>
```

---

# 6. Layout Routes

Purpose:

```txt
Shared UI
```

Examples:

```txt
Header
Sidebar
Footer
Navbar
```

---

Layout Example

```jsx
function Layout() {
  return (
    <>
      <Header />
      <Outlet />
    </>
  );
}
```

---

# 7. Outlet

Purpose:

```txt
Render Child Routes
```

Import:

```jsx
import {
  Outlet
} from "react-router-dom";
```

---

Example:

```jsx
function Layout() {
  return (
    <>
      <Header />

      <Outlet />

    </>
  );
}
```

---

Without Outlet

Problem:

```txt
Child Pages Not Rendering
```

---

# 8. Link

Purpose:

```txt
Navigation
```

Without Page Refresh.

Import:

```jsx
import {
  Link
} from "react-router-dom";
```

---

Example:

```jsx
<Link to="/">
  Home
</Link>
```

---

Wrong:

```jsx
<a href="/">
  Home
</a>
```

Avoid inside React projects.

---

# 9. NavLink

Purpose:

```txt
Active Navigation Styling
```

Import:

```jsx
import {
  NavLink
} from "react-router-dom";
```

---

Example:

```jsx
<NavLink
  to="/cart"
>
  Cart
</NavLink>
```

---

Active Styling

```jsx
<NavLink
  to="/cart"
  className={({ isActive }) =>
    isActive
      ? "active"
      : ""
  }
>
  Cart
</NavLink>
```

---

# 10. Route Parameters

Used For:

```txt
Product Details
User Details
Blog Posts
```

---

Example:

```txt
/product/1
/product/2
/product/3
```

---

Route:

```jsx
{
  path: "product/:id",
  element: <ProductDetail />
}
```

---

# 11. useParams

Purpose:

```txt
Read Dynamic URL Values
```

Import:

```jsx
import {
  useParams
} from "react-router-dom";
```

---

Example:

```jsx
const { id } =
  useParams();
```

URL:

```txt
/product/5
```

Result:

```js
id = "5"
```

---

Use In API

```jsx
fetch(
  `https://dummyjson.com/products/${id}`
);
```

---

# 12. useNavigate

Purpose:

```txt
Programmatic Navigation
```

Import:

```jsx
import {
  useNavigate
} from "react-router-dom";
```

---

Example:

```jsx
const navigate =
  useNavigate();
```

---

Navigate To Page

```jsx
navigate("/cart");
```

---

Go Back

```jsx
navigate(-1);
```

---

Checkout Example

```jsx
navigate("/");
```

After:

```txt
Order Placed
```

---

# 13. useLocation

Purpose:

```txt
Current Route Information
```

Import:

```jsx
import {
  useLocation
} from "react-router-dom";
```

---

Example:

```jsx
const location =
  useLocation();
```

---

Current Path

```jsx
location.pathname
```

Example:

```txt
/cart
```

---

# 14. Dynamic Routes

Definition:

```txt
Route Changes Based On URL
```

Example:

```txt
/product/1
/product/2
/product/3
```

---

Route:

```jsx
{
  path: "product/:id",
  element:
    <ProductDetail />
}
```

---

# 15. Nested Routes

Router:

```jsx
{
  path: "/",
  element: <Layout />,
  children: [

  ]
}
```

---

Example:

```jsx
{
  index: true,
  element: <Home />
}
```

---

```jsx
{
  path: "cart",
  element: <Cart />
}
```

---

```jsx
{
  path: "checkout",
  element: <Checkout />
}
```

---

# 16. Not Found Route

Purpose:

```txt
404 Page
```

---

Example:

```jsx
{
  path: "*",
  element:
    <NotFound />
}
```

---

URL:

```txt
/random-route
```

Shows:

```txt
404 Page Not Found
```

---

# 17. Protected Routes

Purpose:

```txt
Authentication
```

---

Example:

```jsx
function ProtectedRoute({
  children
}) {

  const isLoggedIn =
    true;

  if (!isLoggedIn) {
    return (
      <Navigate
        to="/login"
      />
    );
  }

  return children;
}
```

---

Usage:

```jsx
{
  path: "/profile",
  element: (
    <ProtectedRoute>
      <Profile />
    </ProtectedRoute>
  )
}
```

---

# 18. Common Folder Structure

```txt
src/

routes/
│
└── router.jsx

pages/
│
├── Home.jsx
├── ProductDetail.jsx
├── Cart.jsx
├── Checkout.jsx
└── NotFound.jsx

components/
│
├── Layout.jsx
└── Header.jsx
```

---

# 19. Common Mistakes

## Wrong Import

Wrong:

```jsx
import {
 RouterProvider
}
from "react-router";
```

---

Correct:

```jsx
import {
 RouterProvider
}
from "react-router-dom";
```

---

## Missing Outlet

Problem:

```txt
Child Routes Not Rendering
```

Fix:

```jsx
<Outlet />
```

---

## Wrong Children Syntax

Wrong:

```jsx
children=[
]
```

---

Correct:

```jsx
children: [
]
```

---

## Home Route Wrong

Wrong:

```jsx
{
 path: "home"
}
```

---

Preferred:

```jsx
{
 index: true,
 element: <Home />
}
```

---

## Using href

Wrong:

```jsx
<a href="/cart">
```

---

Correct:

```jsx
<Link to="/cart">
```

---

# 20. Debugging Guide

Error:

```txt
No Routes Matched Location
```

Check:

```txt
Route Path
Router Setup
URL
```

---

Error:

```txt
Page Blank
```

Check:

```txt
RouterProvider
Layout
Outlet
```

---

Error:

```txt
Cannot Read Params
```

Check:

```txt
useParams()
Route Parameter
```

---

# 21. Interview Notes

## React Router

```txt
Library Used For Routing
```

---

## Outlet

```txt
Renders Child Routes
```

---

## Link

```txt
Client Side Navigation
```

---

## useNavigate

```txt
Programmatic Navigation
```

---

## useParams

```txt
Access Dynamic Route Values
```

---

## createBrowserRouter

```txt
Modern Router API
```

---

# 22. Copy-Paste Templates

Router File

```jsx
import {
 createBrowserRouter,
 RouterProvider
} from "react-router-dom";

const router =
createBrowserRouter([
 {
  path: "/",
  element: <Layout />,
  children: [
   {
    index: true,
    element: <Home />
   }
  ]
 }
]);

function Router() {
 return (
  <RouterProvider
   router={router}
  />
 );
}

export default Router;
```

---

Layout

```jsx
import {
 Outlet
} from "react-router-dom";

function Layout() {
 return (
  <>
   <Header />
   <Outlet />
  </>
 );
}

export default Layout;
```

---

useNavigate

```jsx
const navigate =
 useNavigate();

navigate("/");
```

---

useParams

```jsx
const { id } =
 useParams();
```

---

Link

```jsx
<Link to="/cart">
 Cart
</Link>
```

---

# 23. Project Checklist

Before Routing:

```txt
□ Install Router

□ Create Pages

□ Create Layout

□ Add Outlet

□ Configure Router

□ Add RouterProvider
```

---

Before Submission:

```txt
□ Home Route Working

□ Product Route Working

□ Cart Route Working

□ Checkout Route Working

□ Dynamic Route Working

□ NotFound Working

□ No Console Errors
```

---

# Golden Rules

1. Always Use createBrowserRouter.
2. Always Wrap App With RouterProvider.
3. Always Use Outlet For Nested Routes.
4. Use Link Instead Of href.
5. Use useNavigate For Redirects.
6. Use useParams For Dynamic Routes.
7. Keep Layout Separate.
8. Create Proper NotFound Page.
9. Test Every Route Manually.
10. Router Errors Are Usually Setup Errors.