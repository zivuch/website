---
title: Generics in Functions and Interfaces
menu_order: 11
post_status: publish
post_excerpt: Learn how to write reusable and type-safe functions and interfaces using TypeScript generics.
taxonomy:
  category:
    - typescript
    - Advanced Guide to TypeScript
  post_tag:
    - typescript
    - generics
    - reusable functions
    - advanced types
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What are Generics?](#what-are-generics)
- [Generic Functions](#generic-functions)
- [Generic Interfaces](#generic-interfaces)
- [Working with Type Parameters](#working-with-type-parameters)
- [Type Inference with Generics](#type-inference-with-generics)
- [Common Use Cases](#common-use-cases)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 11: Generics in Functions and Interfaces](./lesson-11-generics-in-functions-and-interfaces)
- [Lesson 12: Generic Constraints and Default Types](./lesson-12-generic-constraints-and-default-types)
- [Lesson 13: Utility Types: Partial, Pick, Omit, and Record](./lesson-13-utility-types-partial-pick-omit-and-record)
- [Lesson 14: Mapped Types and Keyof](./lesson-14-mapped-types-and-keyof)
- [Lesson 15: Conditional Types and Infer Keyword](./lesson-15-conditional-types-and-infer-keyword)

</div>

</div>

<div class="guru-main" markdown="1">

## What are Generics?

**Generics** allow you to create **flexible, reusable functions, classes, and interfaces** while keeping strong type safety.

Instead of hardcoding a type, you make it a variable:

```ts
function identity<T>(value: T): T {
  return value;
}
```

Here, `T` is a **type parameter**, like a placeholder for the actual type.

---

## Generic Functions

Define a function with a generic type:

```ts
function wrapInArray<T>(value: T): T[] {
  return [value];
}

const strArray = wrapInArray("hello"); // string[]
const numArray = wrapInArray(42);      // number[]
```

The type is inferred automatically based on input.

---

## Generic Interfaces

You can make interfaces generic too:

```ts
interface ApiResponse<T> {
  data: T;
  success: boolean;
}

const userResponse: ApiResponse<{ id: number }> = {
  data: { id: 1 },
  success: true,
};
```

This works great for API types and abstract utilities.

---

## Working with Type Parameters

You can reference generic types **just like variables**:

```ts
function getFirst<T>(arr: T[]): T {
  return arr[0];
}
```

Type parameters can also reference **multiple types**:

```ts
function pair<A, B>(a: A, b: B): [A, B] {
  return [a, b];
}
```

---

## Type Inference with Generics

Most of the time, TypeScript infers the generic for you:

```ts
const name = identity("Lior"); // T is inferred as string
```

But you can also explicitly pass it:

```ts
const explicit = identity<number>(123);
```

---

## Common Use Cases

- **API response wrappers**
- **Reusable utilities** (e.g., filters, maps)
- **Component props in React**
- **Form types and validators**
- **Generic data models**

---

## Summary

- Generics let you build flexible, reusable, type-safe code
- Use `<T>` to define a placeholder type
- Generics work in functions, interfaces, types, and classes
- TypeScript often infers generic types — but you can specify them explicitly

Next up: **Lesson 12 – Generic Constraints and Default Types**, to add control and fallback behavior to your generics.

</div>
