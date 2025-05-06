---
title: Mapped Types and keyof
menu_order: 14
post_status: publish
post_excerpt: Learn how to transform object types dynamically with mapped types and use keyof to reference property names safely.
taxonomy:
  category:
    - typescript
    - Advanced Guide to TypeScript
  post_tag:
    - typescript
    - mapped types
    - keyof
    - dynamic types
    - type transformation
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is `keyof`?](#what-is-keyof)
- [What are Mapped Types?](#what-are-mapped-types)
- [Remapping All Properties](#remapping-all-properties)
- [Customizing Mapped Types](#customizing-mapped-types)
- [Combining with Utility Types](#combining-with-utility-types)
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

## What is `keyof`?

`keyof` is a TypeScript operator that returns a **union of property names** (keys) of a type:

```ts
type User = {
  id: number;
  name: string;
};

type UserKeys = keyof User; // "id" | "name"
```

You can use it to create reusable and safe logic that depends on object structure.

---

## What are Mapped Types?

**Mapped types** allow you to **create new types** by transforming each property in an existing type.

```ts
type ReadonlyUser = {
  readonly [K in keyof User]: User[K];
};
```

This loops over each key `K` in `User` and assigns the same value type, but makes it `readonly`.

---

## Remapping All Properties

You can do a lot with mapped types:

```ts
type Optional<T> = {
  [K in keyof T]?: T[K];
};

type Nullable<T> = {
  [K in keyof T]: T[K] | null;
};
```

These utilities are similar to built-in `Partial<T>`, `Required<T>`, etc.

---

## Customizing Mapped Types

You can modify the keys or filter them using `as` (TypeScript 4.1+):

```ts
type PrefixProps<T> = {
  [K in keyof T as `data-${string & K}`]: T[K];
};

type Product = { id: number; title: string };

type DataAttrs = PrefixProps<Product>;
// { "data-id": number; "data-title": string }
```

---

## Combining with Utility Types

Mapped types can be composed with other utility types:

```ts
type ReadonlyNullable<T> = {
  readonly [K in keyof T]: T[K] | null;
};

type Settings = { darkMode: boolean; language: string };

const config: ReadonlyNullable<Settings> = {
  darkMode: null,
  language: "en"
};
```

---

## Summary

- `keyof` gives you the keys of an object as a union type
- Mapped types let you loop over keys to transform the object
- Use them to create `Readonly`, `Nullable`, or customized types
- Combine with utility types for powerful reusable patterns

Next up: **Lesson 15 – Conditional Types and `infer` Keyword**, where you’ll build logic into your types.

</div>
