---
title: Using Zustand in Server-Side Rendering (Next.js)
menu_order: 17
post_status: publish
post_excerpt: Learn how to safely use Zustand in server-rendered apps like Next.js, with hydration, persistence, and SSR-safe patterns.
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - nextjs
    - ssr
    - react
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why SSR Affects Zustand
- Common Pitfalls in Next.js
- Safe Zustand Store Setup for SSR
- Hydration Strategy with useEffect
- Optional: Using Zustand with `persist` in SSR

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

## Why SSR Affects Zustand

Zustand is **client-side by default**. In SSR frameworks like **Next.js**, you need to be careful:

- State must not be shared across requests
- Some features like `persist` or `devtools` require `window`
- Hydration mismatches can occur if the store is initialized differently on server and client

---

## Common Pitfalls in Next.js

❌ Initializing Zustand store globally (shared across users)  
❌ Accessing `localStorage` in server code  
❌ Using `persist()` or `devtools()` without guarding for `window`

---

## Safe Zustand Store Setup for SSR

Use the **store factory pattern**:

```ts
import { createStore } from "zustand";

type CounterState = {
  count: number;
  inc: () => void;
};

export const createCounterStore = () =>
  createStore<CounterState>((set) => ({
    count: 0,
    inc: () => set((s) => ({ count: s.count + 1 })),
  }));
```

Now use the factory in each environment independently:

```ts
const store = createCounterStore();
```

You can store the instance in `_app.tsx` and pass it through a context or provider.

---

## Hydration Strategy with useEffect

If you use client-only logic, make sure you **hydrate state safely** on the client:

```ts
useEffect(() => {
  useStore.setState({ ready: true }); // example flag
}, []);
```

Or initialize inside the component to avoid mismatches.

---

## Optional: Using Zustand with `persist` in SSR

`persist` uses `localStorage`, which doesn't exist on the server.

You must conditionally enable it:

```ts
const isServer = typeof window === "undefined";

const useSettingsStore = create(
  !isServer
    ? persist(
        (set) => ({
          darkMode: false,
          toggle: () => set((s) => ({ darkMode: !s.darkMode })),
        }),
        { name: "settings" }
      )
    : () => ({ darkMode: false, toggle: () => {} })
);
```

✅ This prevents hydration issues and ensures safe SSR usage.

---

## Summary

- SSR apps must isolate Zustand stores per request
- Avoid global instances and side effects on the server
- Use factory functions and safe hydration techniques
- Guard `persist()` and other browser-only features

---

🎉 That’s the end of the **Advanced Guide to Zustand**!  
Next up: **Lesson 18 – Zustand for Authentication and Session Management**

</div>
