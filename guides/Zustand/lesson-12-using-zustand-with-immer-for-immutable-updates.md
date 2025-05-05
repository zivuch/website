---
title: Using Zustand with Immer for Immutable Updates
menu_order: 12
post_status: publish
post_excerpt: Learn how to use Zustand with Immer to write clean, immutable state updates using mutable-looking code.
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - immer
    - immutable updates
    - middleware
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What Is Immer and Why Use It?
- Zustand’s `immer` Middleware
- Updating Nested State
- Tips and Warnings

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

## What Is Immer and Why Use It?

**Immer** allows you to write _mutative_ code that produces _immutable_ updates under the hood.

```ts
state.user.name = "Ziv"; // This is actually immutable with Immer!
```

This helps especially when:

- Your state is deeply nested
- You want cleaner updates
- You want Redux-like immutability with minimal effort

---

## Zustand’s `immer` Middleware

Zustand has built-in support for Immer via middleware:

```ts
import { create } from "zustand";
import { immer } from "zustand/middleware/immer";

type Todo = { id: number; title: string; done: boolean };

type TodoStore = {
  todos: Todo[];
  toggleTodo: (id: number) => void;
};

export const useTodoStore = create<TodoStore>()(
  immer((set) => ({
    todos: [],
    toggleTodo: (id) =>
      set((state) => {
        const todo = state.todos.find((t) => t.id === id);
        if (todo) todo.done = !todo.done;
      }),
  }))
);
```

> ✅ `state.todos` is _not_ mutated — Immer tracks changes and returns a new immutable object.

---

## Updating Nested State

With Immer, this:

```ts
set((state) => {
  state.user.profile.avatar = "new.png";
});
```

is equivalent to a fully immutable deep copy update.

✅ Clean  
✅ Safe  
✅ Great for forms, trees, and configs

---

## Tips and Warnings

- `immer()` must wrap your store definition
- All mutations must happen **inside** the `set()` function
- You can use Immer with `persist` and `devtools` (wrap them carefully)
  ```ts
  devtools(persist(immer(...)))
  ```

---

## Summary

- Zustand + Immer = clean, immutable updates with mutable syntax
- Great for deeply nested or complex state trees
- Middleware is built-in and easy to apply
- Pair it with other middlewares for real power

---

Next: **Lesson 13 – Using Zustand with Middleware: Logging, Tracking, and Side Effects**

</div>
