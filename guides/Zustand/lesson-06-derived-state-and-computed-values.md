---
title: Derived State and Computed Values
menu_order: 6
post_status: publish
post_excerpt: Learn how to implement computed values inside Zustand stores using memoization or derived logic.
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - computed
    - derived state
    - react
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What is Derived State?
- Static vs Dynamic Computation
- Derived Inside the Store
- Derived Outside the Store
- When to Use Selectors vs Derivation

</div>

<div class="otg" markdown="1">

## On this Guide

- Lesson 01: Introduction to Zustand and Store Basics  
- Lesson 02: Creating Your First Store with TypeScript  
- Lesson 03: Reading and Updating State in React Components  
- Lesson 04: Selectors and Optimizing Renders  
- Lesson 05: Handling Booleans, Counters, and Simple Objects  
- Lesson 06: Derived State and Computed Values  
- Lesson 07: Type Inference and store typing best practices  
- Lesson 08: Custom Hooks and Reusable State Accessors  

</div>

</div>

<div class="guru-main" markdown="1">

## What is Derived State?

**Derived state** is a value calculated from one or more parts of your store — like computed properties in Vue or selectors in Redux Toolkit.

Example:
```ts
isAdult = age >= 18
fullName = firstName + " " + lastName
```

Zustand doesn't provide built-in computed values — you can derive inside or outside the store.

---

## Static vs Dynamic Computation

You can either:

- 📦 Compute values **inside the store** and expose them
- 🧠 Or compute **outside** using selectors in the component

---

## Derived Inside the Store (Simpler)

```ts
type UserStore = {
  firstName: string;
  lastName: string;
  fullName: string;
  update: (firstName: string, lastName: string) => void;
};

const useUserStore = create<UserStore>((set) => ({
  firstName: "Jane",
  lastName: "Doe",
  fullName: "Jane Doe",
  update: (firstName, lastName) =>
    set(() => ({
      firstName,
      lastName,
      fullName: `${firstName} ${lastName}`,
    })),
}));
```

✅ `fullName` is updated whenever `update()` is called.

---

## Derived Outside the Store (Preferred for Complex Logic)

```ts
const fullName = useUserStore((s) => `${s.firstName} ${s.lastName}`);
```

This keeps your store lean and your component reactive.

You can even wrap it:

```ts
const useFullName = () =>
  useUserStore((s) => `${s.firstName} ${s.lastName}`);
```

---

## When to Use Which?

| Strategy | Use When |
|----------|----------|
| Derived inside store | Small, static, tightly bound values |
| Derived outside store | Dynamic logic, expensive computations, better separation |

For complex state trees, it’s better to derive in your UI layer.

---

## Summary

- Derived state is calculated from your store’s data
- You can derive it inside or outside the store
- For small use cases, do it inside; for complex ones, do it via selectors
- Zustand stays flexible and unopinionated — you're in control

---

Next: **Lesson 07 – Type Inference and Store Typing Best Practices**

</div>
