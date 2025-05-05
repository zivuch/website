---
title: Custom Hooks and Reusable State Accessors
menu_order: 8
post_status: publish
post_excerpt: Learn how to create custom Zustand-based hooks to encapsulate logic and keep your components clean.
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - hooks
    - clean architecture
    - state access
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Use Custom Hooks with Zustand?
- Creating Selective Accessors
- Composing Derived State in Hooks
- Naming and Organizing Hooks
- When to Use vs When to Avoid

</div>

<div class="otg" markdown="1">

## On this Guide

- Lesson 01: Introduction to Zustand and Store Basics
- Lesson 02: Creating Your First Store with TypeScript
- Lesson 03: Reading and Updating State in React Components
- Lesson 04: Selectors and Optimizing Renders
- Lesson 05: Handling Booleans, Counters, and Simple Objects
- Lesson 06: Derived State and Computed Values
- Lesson 07: Type Inference and Store Typing Best Practices
- Lesson 08: Custom Hooks and Reusable State Accessors

</div>

</div>

<div class="guru-main" markdown="1">

## Why Use Custom Hooks with Zustand?

Zustand allows direct access to state anywhere, but **custom hooks** help you:

- Avoid repetition
- Apply consistent selectors
- Add memoization or derived logic
- Improve readability in components

---

## Creating Selective Accessors

Instead of repeating this:

```tsx
const bears = useBearStore((s) => s.bears);
const increase = useBearStore((s) => s.increase);
```

You can wrap it:

```ts
export const useBearCount = () => useBearStore((s) => s.bears);
export const useBearActions = () =>
  useBearStore((s) => ({ increase: s.increase, reset: s.reset }));
```

In components:

```tsx
const bears = useBearCount();
const { increase } = useBearActions();
```

---

## Composing Derived State in Hooks

You can also use derived values inside your custom hooks:

```ts
export const useFullName = () =>
  useUserStore((s) => `${s.firstName} ${s.lastName}`);
```

This keeps components lean and moves logic to reusable hooks.

---

## Naming and Organizing Hooks

📁 Recommended structure:

```
/stores
  useUserStore.ts
  useCounterStore.ts
/hooks
  useFullName.ts
  useIsAdult.ts
```

Use `useXyz` naming to stay idiomatic with React.

---

## When to Use vs When to Avoid

✅ Use custom hooks when:

- You're repeating the same selectors/actions
- You need derived logic in multiple places

🚫 Avoid if:

- The logic is simple and used only once
- It would hide critical state flow

---

## Summary

- Custom hooks improve composability and reusability
- Extract selectors, actions, and derived state
- Keep components declarative and focused
- Great for shared logic, clean architecture, and testability

---

🎉 Congrats — you’ve completed the **Basic Guide to Zustand**!  
Next: **Advanced Guide – Lesson 09: Organizing State with Slices and Modular Stores**

</div>
