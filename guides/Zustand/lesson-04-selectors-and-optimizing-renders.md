---
title: Selectors and Optimizing Renders
menu_order: 4
post_status: publish
post_excerpt: Learn how to write efficient selectors in Zustand and prevent unnecessary component re-renders.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - performance
    - selectors
    - react
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What Are Selectors?
- Why Selectors Improve Performance
- Shallow Comparison and Object Selectors
- Using Zustand’s `shallow` Helper
- Common Anti-Patterns to Avoid

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

## What Are Selectors?

In Zustand, a **selector** is the function you pass into your store hook to extract part of the state.

```ts
const bears = useBearStore((state) => state.bears);
```

This is efficient because Zustand will only re-render this component **if `state.bears` changes.**

---

## Why Selectors Improve Performance

Using selectors:
- Prevents subscribing to the entire store
- Minimizes re-renders
- Keeps components lean and reactive

---

## Shallow Comparison and Object Selectors

If you want to select multiple values, Zustand will trigger re-renders **unless** you optimize it with a shallow comparison.

```ts
import { shallow } from 'zustand/shallow';

const { bears, increase } = useBearStore(
  (state) => ({ bears: state.bears, increase: state.increase }),
  shallow
);
```

This avoids re-renders if neither `bears` nor `increase` has changed.

---

## Using Zustand’s `shallow` Helper

Zustand exports a built-in `shallow` function. Use it when:

- You return an object or array in your selector
- You want to skip unnecessary re-renders when values are stable

```ts
import { shallow } from 'zustand/shallow';
```

---

## Common Anti-Patterns to Avoid

❌ **Don’t** destructure the entire store:
```ts
const { bears, increase } = useBearStore(); // BAD
```

✅ Use individual selectors:
```ts
const bears = useBearStore((s) => s.bears);
const increase = useBearStore((s) => s.increase);
```

---

## Summary

- Selectors make Zustand performant and reactive
- Always select only what you need
- Use `shallow` when selecting multiple values
- Avoid full destructuring unless you know what you're doing

---

Next: **Lesson 05 – Handling Booleans, Counters, and Simple Objects**

</div>
