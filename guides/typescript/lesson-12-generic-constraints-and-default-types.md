---
title: Generic Constraints and Default Types
menu_order: 12
post_status: publish
post_excerpt: Learn how to restrict generics using constraints and set default types to make flexible functions safer and easier to use.
taxonomy:
  category:
    - typescript
    - Advanced Guide to TypeScript
  post_tag:
    - typescript
    - generics
    - constraints
    - default types
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Use Constraints?](#why-use-constraints)
- [Using `extends` to Restrict Generics](#using-extends-to-restrict-generics)
- [Accessing Object Properties Safely](#accessing-object-properties-safely)
- [Default Type Parameters](#default-type-parameters)
- [Combining Constraints and Defaults](#combining-constraints-and-defaults)
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

## Why Use Constraints?

Without constraints, generic types can be **anything** — even things that don’t support the operations you want.

```ts
function getLength<T>(value: T): number {
  return value.length; // ❌ Error: T might not have `.length`
}
```

We can fix this with a **constraint**.

---

## Using `extends` to Restrict Generics

You can require that a generic extends a base type:

```ts
function getLength<T extends { length: number }>(value: T): number {
  return value.length;
}
```

Now the function works only with types that have a `.length` property:

```ts
getLength("hello");     // ✅
getLength([1, 2, 3]);    // ✅
getLength(123);          // ❌ Error
```

---

## Accessing Object Properties Safely

You can ensure that a key exists on an object using `keyof`:

```ts
function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Lior", age: 30 };

getProp(user, "name"); // "Lior"
getProp(user, "email"); // ❌ Error: Property does not exist
```

This makes your generic functions **type-safe** and **self-validating**.

---

## Default Type Parameters

You can provide a default if the caller doesn’t supply one:

```ts
type ApiResponse<T = any> = {
  data: T;
  error?: string;
};

const res: ApiResponse = {
  data: "fallback type is any",
};
```

This is useful for utilities or when you want to provide a **sensible fallback**.

---

## Combining Constraints and Defaults

You can use both together:

```ts
function identity<T extends string | number = string>(value: T): T {
  return value;
}

identity("test"); // ok
identity(123);    // ok
identity(true);   // ❌ Error: boolean not allowed
```

---

## Summary

- Use `extends` to restrict generics to specific shapes or types
- Use `keyof` and indexed types to safely access object properties
- Provide **default types** for simpler usage and better fallback
- Combining constraints and defaults gives you control **and** flexibility

Next up: **Lesson 13 – Utility Types: Partial, Pick, Omit, and Record** — learn how to transform types like a pro.

</div>
