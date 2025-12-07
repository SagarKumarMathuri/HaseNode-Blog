---
title: "🚀 React Code Splitting: Boost Performance by Loading Only What You Need"
datePublished: Sun Dec 07 2025 19:09:43 GMT+0000 (Coordinated Universal Time)
cuid: cmiw3k1pc000002jy01ld9p9a
slug: react-code-splitting-boost-performance-by-loading-only-what-you-need
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Im7lZjxeLhg/upload/847bbf9316636ddcacaa78ed765315ec.jpeg
tags: react-code-splitting

---

Modern React apps grow quickly — more routes, more components, more dependencies.  
But here’s the problem:

👉 **Bigger bundle = Slower load time = Bad user experience**

Enter **Code Splitting** — one of the easiest ways to optimise performance in React.

In this blog, you’ll learn:

* What Code Splitting is
    
* Why it matters
    
* How to use `React.lazy()` & `Suspense`
    
* Route-based & Component-based code splitting
    
* Best practices
    

---

# 🧠 What is Code Splitting?

**Code Splitting** means breaking your app into smaller bundles that load only when needed.

This prevents loading everything at once during the initial render.

### Without Code Splitting

React loads:  
✔ All components  
✔ All routes  
✔ All library code  
✔ Even pages user may never open!

### With Code Splitting

React loads only:  
✔ Initial route (Home)  
✔ Other pages/components loaded lazily *when needed*

Result ➝ Faster load ⏩ Better UX ⭐ Better Lighthouse score 📈

---

# 💡 How React Supports Code Splitting

React provides built-in APIs:

### 1️⃣ `React.lazy()`

Used to load a component lazily.

### 2️⃣ `Suspense`

Used to show a fallback (like a loader) while the component is loading.

---

# ▶️ Basic Example: Lazy Loading a Component

```apache
import React, { Suspense, lazy } from "react";

const About = lazy(() => import("./About"));

function App() {
  return (
    <div>
      <h1>React Code Splitting</h1>

      <Suspense fallback={<p>Loading...</p>}>
        <About />
      </Suspense>
    </div>
  );
}

export default App;
```

### 🔍 What’s happening?

* `About` component is **not** bundled in the main file
    
* It loads **only when rendered**
    
* `Suspense` shows a *loading placeholder*
    

---

# 🔥 Route-Based Code Splitting (React Router)

This is the most common use case.

```apache
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { Suspense, lazy } from "react";

const Home = lazy(() => import("./pages/Home"));
const Profile = lazy(() => import("./pages/Profile"));
const Contact = lazy(() => import("./pages/Contact"));

function App() {
  return (
    <BrowserRouter>
      <Suspense fallback={<h2>Loading Page...</h2>}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/profile" element={<Profile />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </Suspense>
    </BrowserRouter>
  );
}

export default App;
```

💡 Each route becomes a **separate bundle**.  
When the user visits `/profile`, only then React loads `Profile.js`.

---

# ✔ Code Splitting for Modules (Charts, Editors, Maps)

If you have heavy libraries (Chart.js, Leaflet, Rich Editors), lazy loading saves **MBs**.

Example: Lazy loading a chart component.

```apache
const ChartComponent = lazy(() => import("./ChartComponent"));
```

Use inside Suspense:

```apache
<Suspense fallback={<Spinner />}>
  <ChartComponent />
</Suspense>
```

---

# 🧩 Splitting Large Lists or Components

If a component is rarely used, make it lazy:

```apache
const UserDetails = lazy(() => import("./UserDetails"));
```

Render:

```apache
{showDetails && (
  <Suspense fallback={<Loader />}>
    <UserDetails />
  </Suspense>
)}
```

---

# ⚙ Dynamic Import with Conditions (Advanced)

```apache
let Component;

if (user.role === "admin") {
  Component = lazy(() => import("./AdminPanel"));
} else {
  Component = lazy(() => import("./UserDashboard"));
}
```

Show a fallback:

```apache
<Suspense fallback={<p>Loading dashboard...</p>}>
  <Component />
</Suspense>
```

---

# 🚧 Common Mistakes to Avoid

❌ Don’t wrap `Suspense` around too large parts of the app  
✔ Wrap around lazy components only

❌ Calling lazy inside loops  
✔ Always define lazy at the top

❌ Forgetting fallback  
✔ Always define a simple loader

❌ Creating thousands of tiny chunks  
✔ Split only heavy or independent modules

---

# 🏆 Best Practices

✔ Split large routes (`/about`, `/contact`)  
✔ Lazy load admin dashboards  
✔ Lazy load rarely visited components  
✔ Lazy load heavy UI libraries  
✔ Test with Lighthouse or Webpack bundle analyzer  
✔ Use `Suspense` boundaries near lazy imports

---

# 📈 Benefits of Code Splitting

| Benefit | Description |
| --- | --- |
| 🚀 Faster Load | Smaller initial bundle |
| 🎯 Better UX | User sees content faster |
| 📉 Lower Data Usage | Loads only required code |
| 🔧 Optimized App | Better mobile performance |
| 🌐 SEO Friendly | Faster page load improves ranking |

---

# 🎉 Final Thoughts

React Code Splitting is a **must-use technique** for any modern frontend app.  
It improves performance, speeds up load time, and offers a smoother experience.