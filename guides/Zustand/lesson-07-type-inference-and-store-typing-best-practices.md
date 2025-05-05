---
title: Type Inference and Store Typing Best Practices
menu_order: 7
post_status: publish
post_excerpt: Master Zustand typing patterns using generics, type inference, and reusable store types.
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - typescript
    - typing
    - best practices
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Typing a Zustand Store with Generics
- How to Use z.infer-like Patterns
- Avoiding Over-Annotation
- Reusing Store Types in Components

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

## Typing a Zustand Store with Generics

Zustand's `create()` accepts a generic type that represents your full store shape:

```ts
type CounterStore = {
  count: number;
  inc: () => void;
};

const useCounterStore = create<CounterStore>((set) => ({
  count: 0,
  inc: () => set((s) => ({ count: s.count + 1 })),
}));
```

✅ This gives you autocomplete, type checking, and error safety across your app.

---

## How to Use `typeof` for Inference

Instead of repeating types, infer from the store itself:

```ts
const useUserStore = create<{
  name: string;
  setName: (name: string) => void;
}>((set) => ({
  name: "",
  setName: (name) => set({ name }),
}));

export type UserStore = ReturnType<typeof useUserStore>;
```

This gives you access to the shape of your store anywhere else in your app.

---

## Avoiding Over-Annotation

You don’t need to overtype every state update.

❌ Too much:
```ts
set((state: CounterStore) => ({ count: state.count + 1 }));
```

✅ Just let TypeScript infer:
```ts
set((s) => ({ count: s.count + 1 }));
```

---

## Reusing Store Types in Components

Export your store’s type if it helps with testing or props:

```ts
export type CounterStore = {
  count: number;
  inc: () => void;
};
```

Then use it elsewhere:

```ts
const MyButton: FC<{ store: CounterStore }> = ({ store }) => (
  <button onClick={store.inc}>Click</button>
);
```

---

## Summary

- Always use `<T>` with `create()` to ensure type-safe stores
- Use `ReturnType<typeof useStore>` to infer full types
- Don’t over-annotate — let TS infer where possible
- Export your store types for maximum reuse

---

Next: **Lesson 08 – Custom Hooks and Reusable State Accessors**

</div>
