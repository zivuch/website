---
title: Using Devtools Middleware for Debugging
menu_order: 11
post_status: publish
post_excerpt: Learn how to connect your Zustand store to Redux DevTools and gain insight into state changes and actions.
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - devtools
    - debugging
    - middleware
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Use Devtools with Zustand?
- Setting Up `devtools` Middleware
- Naming Actions and Stores
- Tracking State Changes
- Tips and Gotchas

</div>

<div class="otg" markdown="1">

## On this Guide

- Lesson 09: Organizing State with Slices and Modular Stores
- Lesson 10: Persisting State to localStorage or sessionStorage
- Lesson 11: Using Devtools Middleware for Debugging
- Lesson 12: Using Zustand with Immer for Immutable Updates
- Lesson 13: Using Zustand with Middleware: Logging, Tracking, and Side Effects
- Lesson 14: Subscribing to External State Changes
- Lesson 15: Creating Read-Only or Transient State Stores
- Lesson 16: Testing Zustand Stores with React Testing Library
- Lesson 17: Using Zustand in Server-Side Rendering (Next.js)

</div>

</div>

<div class="guru-main" markdown="1">

## Why Use Devtools with Zustand?

Zustand has built-in support for **Redux DevTools**. This gives you:

- 🔍 Real-time inspection of your store’s state
- 🕹️ Playback of actions and state changes
- 📈 Time-travel debugging

It’s optional, but very helpful during development.

---

## Setting Up `devtools` Middleware

First, wrap your store with the `devtools` middleware:

```ts
import { create } from "zustand";
import { devtools } from "zustand/middleware";

type CounterStore = {
  count: number;
  inc: () => void;
};

export const useCounterStore = create<CounterStore>()(
  devtools(
    (set) => ({
      count: 0,
      inc: () => set((s) => ({ count: s.count + 1 }), false, "inc"),
    }),
    { name: "CounterStore" }
  )
);
```

> 🔍 Tip: The third argument to `set` is an action name — it shows up in DevTools!

---

## Naming Actions and Stores

Use the `name` option for the devtools plugin:

```ts
devtools((set) => ({ ... }), { name: "SettingsStore" });
```

And label your actions clearly inside `set()`:

```ts
set((s) => ({ darkMode: !s.darkMode }), false, "toggleDarkMode");
```

---

## Tracking State Changes

Once configured, open your browser's Redux DevTools panel. You’ll see:

- Actions like `inc`, `reset`, `toggleDarkMode`
- Snapshots of state at every update
- The ability to jump between past states

---

## Tips and Gotchas

✅ Use **action labels** for clarity  
✅ Use `process.env.NODE_ENV === "development"` to avoid loading devtools in production  
✅ Combine with `persist` middleware (but wrap `devtools(persist(...))`)  
✅ Ensure Redux DevTools extension is installed in your browser

```ts
if (process.env.NODE_ENV === "development") {
  // Apply devtools only in dev
}
```

---

## Summary

- Zustand can connect directly to Redux DevTools using `devtools` middleware
- Helps visualize, debug, and rewind your state history
- Great for development; avoid including in production builds

---

Next: **Lesson 12 – Using Zustand with Immer for Immutable Updates**

</div>
