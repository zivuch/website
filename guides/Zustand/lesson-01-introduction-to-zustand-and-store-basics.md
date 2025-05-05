---
title: Introduction to Zustand and Store Basics
menu_order: 1
post_status: publish
post_excerpt: Learn what Zustand is, why it's useful, and how to set up your first store in under a minute.
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - react
    - state management
    - typescript
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What is Zustand?
- Why Choose Zustand?
- Basic Store Example
- Setup Requirements

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 01: Introduction to Zustand and Store Basics](./lesson-01-introduction-to-zustand-and-store-basics)
- [Lesson 02: Creating Your First Store with TypeScript](./lesson-02-creating-your-first-store-with-typescript)
- [Lesson 03: Reading and Updating State in React Components](./lesson-03-reading-and-updating-state-in-react-components)
- [Lesson 04: Selectors and Optimizing Renders](./lesson-04-selectors-and-optimizing-renders)
- [Lesson 05: Handling Booleans, Counters, and Simple Objects](./lesson-05-handling-booleans-counters-and-simple-objects)
- [Lesson 06: Derived State and Computed Values](./lesson-06-derived-state-and-computed-values)
- [Lesson 07: Type Inference and Store Typing Best Practices](./lesson-07-type-inference-and-store-typing-best-practices)
- [Lesson 08: Custom Hooks and Reusable State Accessors](./lesson-08-custom-hooks-and-reusable-state-accessors)

</div>

</div>

<div class="guru-main" markdown="1">

## What is Zustand?

**Zustand** (German for "state") is a small, fast, and scalable state management library for React. It provides a simple, minimal API to manage both local and global state without the boilerplate of Redux or the complexity of Context.

Zustand is created by the team behind Jotai and React Spring, and it focuses on:

- ✅ Simplicity
- ✅ Performance (no provider needed)
- ✅ Full TypeScript support
- ✅ Middleware and plugin extensibility

---

## Why Choose Zustand?

- No context provider necessary
- Centralized state logic (or split into slices)
- Built-in middleware support (devtools, persistence, immer)
- Great for both simple and complex apps
- Works with SSR frameworks like **Next.js**

> Zustand gives you a Redux-like store experience without the ceremony.

---

## Basic Store Example

Here’s how easy it is to create a Zustand store:

```ts
import { create } from "zustand";

type BearState = {
  bears: number;
  increase: () => void;
};

const useBearStore = create<BearState>((set) => ({
  bears: 0,
  increase: () => set((state) => ({ bears: state.bears + 1 })),
}));
```

You can use it directly in your component:

```tsx
function BearCounter() {
  const bears = useBearStore((state) => state.bears);
  return <h1>{bears} bears</h1>;
}
```

---

## Setup Requirements

Install Zustand using your package manager:

```bash
npm install zustand
# or
yarn add zustand
```

If you're using TypeScript, Zustand supports types out-of-the-box. No special typings are needed for basic usage.

---

✅ You now have Zustand running with a simple counter example.

Next: **Lesson 02 – Creating Your First Store with TypeScript**

</div>
