# 🚀 React + Vite Project Setup Playbook

This document serves as the definitive guide and checklist for spinning up a production-ready React application using Vite from scratch. Follow these steps sequentially to ensure a solid architectural foundation before writing feature code.

---

## 📦 1. Core Project Creation (Vite)

### Create the Project
```bash
# Scaffolds a new project interactively
npm create vite@latest my-project -- --template react

# Alternative (interactive manual selection):
# npm create vite@latest
```
* **Select:** `React`
* **Select:** `JavaScript` (or `TypeScript` if migrating)

### Initialization Sequence
```bash
cd my-project
npm install
npm run dev
```

### Build & Preview Verification
```bash
npm run build
npm run preview
```

---

## 🌿 2. Version Control Setup (Git & GitHub)

### Local Initialization
```bash
git init
git status
git add .
git commit -m "chore: initial commit from Vite scratch"
```

### Remote Repository Connection
1. Create a blank repository on GitHub (do **not** initialize with README or license).
2. Link and push using the following sequence:

```bash
# Connect local to remote
git remote add origin [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)

# Verify the connection
git remote -v

# Rename default branch to main and push
git branch -M main
git push -u origin main
```

---

## 🔒 3. Environment & Git Ignores (`.gitignore`)

Ensure your `.gitignore` file contains the following entries immediately to protect credentials and heavy directories:

```text
# Dependencies
node_modules/
/.pnp
.pnp.js

# Production builds
dist/
build/

# Environment variables & secrets
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# Debug logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*
```

> 💡 **Pro-Tip:** Always create a `.env.example` file in the root containing placeholder values (e.g., `VITE_API_URL=your_api_url_here`) so team members know which variables are required without exposing actual secrets.

---

## 🛠️ 4. Essential Ecosystem Installation

### Navigation & State Management
```bash
# React Router for multi-page management
npm install react-router-dom

# Redux Toolkit for predictable global state
npm install @reduxjs/toolkit react-redux
```

### Styling (Tailwind CSS v4)
```bash
npm install tailwindcss @tailwindcss/vite
```

#### `vite.config.js` Configuration
```javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
  ],
});
```

#### `src/index.css` Injection
```css
@import "tailwindcss";
```

### Common Utility Packages
```bash
# API Fetching
npm install axios

# Notification UI
npm install react-toastify

# Vector Icons
npm install react-icons

# High-performance Form Handling
npm install react-hook-form
```

---

## 🗂️ 5. Recommended Architecture & Directory Structure

```text
src/
│
├── app/                  # Application wrappers & configurations
│   └── store.js          # Central Redux Store setup
│
├── redux/                # Global State Slices
│   └── authSlice.js      # Example state feature
│
├── hooks/                # Custom React Hooks (e.g., useAuth, useFetch)
│
├── pages/                # High-level route views (Home, Dashboard, Login)
│
├── components/           # Reusable Presentational UI Components
│   ├── common/           # Buttons, Loaders, Input inputs
│   └── layout/           # Header, Footer, Sidebar, Layout container
│
├── routes/               # Routing configurations & route guards
│   └── AppRoutes.jsx
│
├── services/             # API clients, Axios instances, endpoint definitions
│   └── api.js
│
├── utils/                # Pure helper functions, formatting, constants
│
├── styles/               # Global custom CSS configurations
│
├── App.jsx               # Entry-level Component Shell
└── main.jsx              # DOM Mount initialization point
```

---

## 🧱 6. Core Structural Components

Every production boilerplate requires a base structural layout before features are built.

### Component Checklist
* [ ] **Layout:** Outer shell handling headers, footers, and persistent wrappers.
* [ ] **Header / Navbar:** Top application branding and navigation triggers.
* [ ] **Loader / Spinner:** Clean user feedback for async fetching gaps.
* [ ] **ErrorMessage:** Graceful error boundary fallback component.
* [ ] **NotFound (404):** Catch-all route page layout.

---

## 🔢 7. Atomic Setup Git Commit Sequence

Break up your initialization configuration into clear, semantic atomic commits:

```bash
git add . && git commit -m "chore: initialize Vite React project"
git add . && git commit -m "chore: install React Router DOM and Redux Toolkit"
git add . && git commit -m "chore: configure Tailwind CSS v4 pipeline"
git add . && git commit -m "chore: scaffold recommended folder structure"
git add . && git commit -m "feat: configure application layout and global routing boundaries"
git add . && git commit -m "feat: build and provide central Redux store setup"
```

---

## 🚨 8. Debugging Manual & Common Pitfalls

| Error Signature | Root Cause | Immediate Fix |
| :--- | :--- | :--- |
| `Cannot find module '...'` | Node modules are missing or out of sync. | Run `npm install` |
| `Could not find react-redux context value...` | Components trying to use Redux hooks outside of a parent Context Provider. | Wrap your `<App />` component inside `<Provider store={store}>` inside `main.jsx`. |
| `No routes matched location` | Path routing matches nothing or path parsing is corrupt. | Check your route declarations and fallback paths. |
| Child UI elements are entirely invisible | Missing routing window renderer in layouts. | Ensure `<Outlet />` from `react-router-dom` is included inside your wrapper `Layout` component. |
| Router imports bringing compilation errors | Utilizing wrong entry pathing. | **Wrong:** `react-router`<br>**Correct:** `react-router-dom` |

---

## 🏁 9. Pre-Flight Verification Checklist

Before you write your very first feature branch line item, check off the following parameters:

- [ ] `npm run dev` boots locally with no errors.
- [ ] `npm run build` transpiles production bundles flawlessly.
- [ ] `.env` files are fully hidden and verified absent via `git status`.
- [ ] Browser developer console contains **zero** red error stack traces.
- [ ] Production routing wrappers redirect unexpected routes directly to `NotFound`.
- [ ] Git remote tracking matches up exactly to target production organization repositories.

> 🏆 **The Golden Rule:** Never compromise your scaffolding. Setup routing, state store injection, UI frameworks, and clean standard folder footprints *before* starting actual UI or feature development. Complete foundations first.
```