---
title: Creating Your First Store with TypeScript
menu_order: 2
post_status: publish
post_excerpt: Learn how to define a strongly typed Zustand store and access it safely in React using TypeScript.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - react
    - typescript
    - state management
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- TypeScript Store Structure
- Setting State with Type Safety
- Accessing Store Values in React
- Best Practice Tips

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

## TypeScript Store Structure

Zustand makes it easy to type your store.

Start by defining a TypeScript interface for your store:

```ts
type BearStore = {
  bears: number;
  increase: () => void;
  reset: () => void;
};
```

Now use it in `create()`:

```ts
import { create } from 'zustand';

const useBearStore = create<BearStore>((set) => ({
  bears: 0,
  increase: () => set((state) => ({ bears: state.bears + 1 })),
  reset: () => set({ bears: 0 }),
}));
```

---

## Accessing Store Values in React

In a component, use Zustand hooks like this:

```tsx
function Controls() {
  const { increase, reset } = useBearStore();
  return (
    <>
      <button onClick={increase}>+1</button>
      <button onClick={reset}>Reset</button>
    </>
  );
}

function BearCounter() {
  const bears = useBearStore((state) => state.bears);
  return <h2>{bears} bears around</h2>;
}
```

You get:
- Full type safety
- Autocomplete in VSCode
- No boilerplate

---

## Best Practice Tips

✅ Always define a type or interface for your store  
✅ Avoid `any` — Zustand supports generics cleanly  
✅ Use function signatures (`() => void`) for actions  
✅ Use arrow functions inside `set()` to access previous state

---

## Summary

- Zustand integrates cleanly with TypeScript
- Define a type, then pass it to `create<YourType>()`
- Typed actions make your app safer and easier to maintain

---

Next: **Lesson 03 – Reading and Updating State in React Components**

</div>
