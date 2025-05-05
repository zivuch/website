---
title: Organizing State with Slices and Modular Stores
menu_order: 9
post_status: publish
post_excerpt: Learn how to scale your Zustand stores by splitting state logic into modular, composable slices.
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - architecture
    - slices
    - modular
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What Are Zustand Slices?
- Creating a Slice-Based Store
- Typing Slices in TypeScript
- Best Practices for Modularization
- When to Use Slices

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

## What Are Zustand Slices?

**Slices** are a pattern for splitting a large Zustand store into multiple focused parts — or "slices" — of state logic. Each slice handles one concern (e.g., `user`, `cart`, `ui`) and can be composed into a single store.

✅ Clean  
✅ Scalable  
✅ Type-safe

---

## Creating a Slice-Based Store

Start by defining separate slice creators:

```ts
// userSlice.ts
export type UserSlice = {
  name: string;
  setName: (name: string) => void;
};

export const createUserSlice = (
  set: (partial: Partial<UserSlice>) => void
): UserSlice => ({
  name: "",
  setName: (name) => set({ name }),
});
```

```ts
// cartSlice.ts
export type CartSlice = {
  items: string[];
  addItem: (item: string) => void;
};

export const createCartSlice = (
  set: (fn: (state: any) => any) => void
): CartSlice => ({
  items: [],
  addItem: (item) => set((state) => ({ items: [...state.items, item] })),
});
```

---

## Composing the Store

Combine the slices in your main store file:

```ts
import { create } from "zustand";
import { createUserSlice, UserSlice } from "./userSlice";
import { createCartSlice, CartSlice } from "./cartSlice";

type StoreState = UserSlice & CartSlice;

export const useAppStore = create<StoreState>()((...a) => ({
  ...createUserSlice(...a),
  ...createCartSlice(...a),
}));
```

Now use it anywhere:

```ts
const name = useAppStore((s) => s.name);
const addItem = useAppStore((s) => s.addItem);
```

---

## Typing Slices in TypeScript

Each slice defines its own type (e.g. `UserSlice`, `CartSlice`)  
The main store uses a union of all slice types.

This helps keep:

- Interfaces small and focused
- Stores highly composable

---

## Best Practices for Modularization

- 🔹 One slice = one file (or folder if complex)
- 🔹 Avoid tightly coupling slices (no cross-slice access)
- 🔹 Export each slice's type and creator separately
- 🔹 Keep actions close to state

---

## When to Use Slices

Use slices when:

- Your store is growing large
- You want better code splitting
- You work in teams or feature modules

---

## Summary

- Zustand slices let you modularize large stores
- Use `createSlice()` functions with shared `set()` logic
- Compose multiple slices into a single typed store
- Perfect for scalable, enterprise-grade Zustand apps

---

Next: **Lesson 10 – Persisting State to localStorage or sessionStorage**

</div>
