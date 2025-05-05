---
title: Reading and Updating State in React Components
menu_order: 3
post_status: publish
post_excerpt: Learn how to read state, trigger updates, and structure Zustand hooks inside your React components.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - react
    - state
    - typescript
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Reading State with Selectors
- Updating State from Events
- Destructuring vs Selecting
- Render Optimization Tips

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

## Reading State with Selectors

Zustand uses a hook-based API to access store values:

```tsx
const bears = useBearStore((state) => state.bears);
```

You can safely use this in your JSX:

```tsx
function BearCounter() {
  const bears = useBearStore((state) => state.bears);
  return <h2>Bears: {bears}</h2>;
}
```

Each call to `useBearStore` subscribes your component to that part of the state.

---

## Updating State from Events

Actions in your store (like `increase()`) are just functions:

```tsx
function IncreaseButton() {
  const increase = useBearStore((state) => state.increase);
  return <button onClick={increase}>+1 Bear</button>;
}
```

Zustand gives you full freedom to use store logic **anywhere in your component tree** — no need for context providers.

---

## Destructuring vs Selecting

❌ Avoid this:

```tsx
const { bears, increase } = useBearStore(); // BAD
```

✅ Instead, select exactly what you need:

```tsx
const bears = useBearStore((state) => state.bears);
const increase = useBearStore((state) => state.increase);
```

This reduces unnecessary re-renders.

---

## Render Optimization Tips

- ✅ Use one selector per value to avoid re-renders
- ✅ Don't destructure the entire state — only subscribe to what you use
- ✅ Use shallow comparison (`shallow`) when selecting multiple values

```ts
import { shallow } from 'zustand/shallow';

const { bears, increase } = useBearStore(
  (state) => ({ bears: state.bears, increase: state.increase }),
  shallow
);
```

---

## Summary

- Read store values in React using `useStore((state) => state.key)`
- Trigger updates by calling actions
- Optimize renders by selecting only what's needed
- Zustand makes state access feel just like React hooks — because it is

---

Next: **Lesson 04 – Selectors and Optimizing Renders**

</div>
