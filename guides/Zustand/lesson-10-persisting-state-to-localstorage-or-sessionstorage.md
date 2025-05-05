---
title: Persisting State to localStorage or sessionStorage
menu_order: 10
post_status: publish
post_excerpt: Learn how to use Zustand’s persist middleware to store and rehydrate state using localStorage or sessionStorage.
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - persistence
    - middleware
    - localstorage
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Use Persistence?
- Installing the Middleware
- Setting Up Zustand with `persist`
- Custom Storage Engines (sessionStorage, async)
- Debugging and Gotchas

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

## Why Use Persistence?

State persistence helps your app:

- ✅ Keep data across refreshes
- ✅ Restore user preferences or sessions
- ✅ Enable offline-first features

Zustand provides a built-in `persist` middleware to handle this elegantly.

---

## Installing the Middleware

Zustand’s `persist` middleware is included by default:

```bash
npm install zustand
```

No extra package is needed. It's part of the core.

---

## Setting Up Zustand with `persist`

Here's an example of persisting a simple settings store:

```ts
import { create } from "zustand";
import { persist } from "zustand/middleware";

type SettingsStore = {
  darkMode: boolean;
  toggleDarkMode: () => void;
};

export const useSettingsStore = create<SettingsStore>()(
  persist(
    (set) => ({
      darkMode: false,
      toggleDarkMode: () => set((state) => ({ darkMode: !state.darkMode })),
    }),
    {
      name: "settings-storage", // unique key in localStorage
    }
  )
);
```

✅ Now `darkMode` will survive page reloads.

---

## Custom Storage Engines (sessionStorage, Async)

You can customize the storage engine:

```ts
persist(
  (set) => ({
    /* your store */
  }),
  {
    name: "my-store",
    storage: {
      getItem: (name) => sessionStorage.getItem(name),
      setItem: (name, value) => sessionStorage.setItem(name, value),
      removeItem: (name) => sessionStorage.removeItem(name),
    },
  }
);
```

You can even use AsyncStorage (for React Native) or a server adapter.

---

## Debugging and Gotchas

⚠️ **Common issues:**

- Double hydration if SSR is used (see Lesson 17)
- Forgetting to use `persist()` inside a `.ts()` call
- Key conflicts in storage — use unique names!

✅ Use devtools or inspect your browser’s localStorage to confirm it's working.

---

## Summary

- Use `persist()` to store state in `localStorage` or `sessionStorage`
- Keeps user preferences or session state across page reloads
- Works with any slice or store, no extra libraries needed
- Customize the storage backend for full control

---

Next: **Lesson 11 – Using Devtools Middleware for Debugging**

</div>
