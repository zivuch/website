---
title: Using Zustand with Middleware: Logging, Tracking, and Side Effects
menu_order: 13
post_status: publish
post_excerpt: Learn how to extend Zustand stores with custom middleware for logging actions, tracking state changes, and managing side effects.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - middleware
    - logging
    - side effects
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What is Middleware in Zustand?
- Creating a Logging Middleware
- Composing Multiple Middleware Layers
- When and Where to Use Middleware
- Example: Action Tracking in Production

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

## What is Middleware in Zustand?

Middleware in Zustand lets you **enhance or wrap** your store behavior by intercepting:

- Actions (`set`)
- State updates
- Store creation

Zustand includes built-in middleware like `devtools`, `persist`, and `immer`, but you can also write your own.

---

## Creating a Logging Middleware

Here's how to create a simple logger:

```ts
import { StateCreator } from "zustand";

const logger =
  <T>(config: StateCreator<T>): StateCreator<T> =>
  (set, get, api) =>
    config(
      (args) => {
        console.log("[Zustand] Action:", args);
        set(args);
      },
      get,
      api
    );
```

Use it like this:

```ts
const useStore = create<TodoStore>()(
  logger((set) => ({
    todos: [],
    addTodo: (text) => set((s) => ({ todos: [...s.todos, { text }] })),
  }))
);
```

---

## Composing Multiple Middleware Layers

You can compose multiple layers easily:

```ts
import { devtools, persist, immer } from "zustand/middleware";

create(
  devtools(
    persist(
      immer(
        logger((set) => ({
          count: 0,
          inc: () => set((s) => ({ count: s.count + 1 })),
        }))
      ),
      { name: "counter" }
    )
  )
);
```

Order matters: outermost wraps everything.

---

## When and Where to Use Middleware

✅ Use middleware for:

- Analytics & logging
- Debugging
- Custom storage or side effects
- Code organization (ex: splitting effects vs state)

🚫 Avoid using middleware for:

- Rendering or UI-related logic
- Over-complicating small stores

---

## Example: Tracking Actions in Production

You can send store actions to analytics:

```ts
const tracking =
  <T>(config: StateCreator<T>): StateCreator<T> =>
  (set, get, api) =>
    config(
      (args) => {
        if (process.env.NODE_ENV === "production") {
          sendToAnalytics(args); // e.g., LogRocket, Segment, etc.
        }
        set(args);
      },
      get,
      api
    );
```

---

## Summary

- Zustand middleware gives you clean extensibility
- Use it for logging, analytics, debugging, and advanced state behavior
- You can create and stack your own middleware
- Middleware logic stays separate from UI

---

Next: **Lesson 14 – Subscribing to External State Changes**

</div>
