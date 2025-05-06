---
title: Conditional Types and Infer Keyword
menu_order: 15
post_status: publish
post_excerpt: Learn how to build dynamic, logic-driven types in TypeScript using conditional types and the infer keyword.
taxonomy:
  category:
    - typescript
    - Advanced Guide to TypeScript
  post_tag:
    - typescript
    - conditional types
    - infer
    - advanced types
    - type logic
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What Are Conditional Types?](#what-are-conditional-types)
- [Basic Syntax](#basic-syntax)
- [Practical Use Cases](#practical-use-cases)
- [Using `infer` to Extract Types](#using-infer-to-extract-types)
- [Distributive Conditional Types](#distributive-conditional-types)
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

## What Are Conditional Types?

Conditional types let you define types **based on a condition**:

```ts
T extends U ? X : Y
```

If `T` extends `U`, the result is type `X`; otherwise, it is `Y`.

---

## Basic Syntax

```ts
type IsString<T> = T extends string ? "yes" : "no";

type A = IsString<string>; // "yes"
type B = IsString<number>; // "no"
```

This is great for **type-based logic** and transformations.

---

## Practical Use Cases

### Strip `null` from a type:

```ts
type NonNullable<T> = T extends null | undefined ? never : T;

type A = NonNullable<string | null>; // string
```

### Check if type is an array:

```ts
type IsArray<T> = T extends any[] ? true : false;

type X = IsArray<string[]>; // true
type Y = IsArray<number>;   // false
```

---

## Using `infer` to Extract Types

`infer` lets you **pull out a type from a structure**:

```ts
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type Result = ReturnType<() => number>; // number
```

This is how TypeScript internally builds types like `ReturnType`, `Parameters`, `ConstructorParameters`, etc.

---

## Distributive Conditional Types

Conditional types are **distributive** over unions by default:

```ts
type ToString<T> = T extends number ? string : never;

type X = ToString<1 | 2 | boolean>; // string | never → string
```

To disable this behavior, wrap the type in a tuple:

```ts
type NonDist<T> = [T] extends [number] ? string : boolean;

type A = NonDist<1 | 2>; // boolean (not distributed)
```

---

## Summary

- Use conditional types to express **type-level logic**
- `T extends U ? X : Y` gives you conditional output types
- `infer` lets you **extract inner types** like return values, parameters, etc.
- Mastering this unlocks true **meta-programming with types**

🎉 You’ve now completed the **Advanced Guide to TypeScript**.

Coming next: **Practical Guide to TypeScript – Real-world use cases with React, Node.js, APIs, and more.**

</div>
