---
title: Type Aliases vs Interfaces
menu_order: 8
post_status: publish
post_excerpt: Understand the differences between type aliases and interfaces, and learn when to use each in your TypeScript projects.
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - type alias
    - interface
    - object typing
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is a Type Alias?](#what-is-a-type-alias)
- [What is an Interface?](#what-is-an-interface)
- [Key Differences](#key-differences)
- [When to Use Type vs Interface](#when-to-use-type-vs-interface)
- [Can You Combine Them?](#can-you-combine-them)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 01: What is TypeScript and Why Use It](./lesson-01-what-is-typescript-and-why-use-it)
- [Lesson 02: Setting Up TypeScript in Your Project](./lesson-02-setting-up-typescript-in-your-project)
- [Lesson 03: Basic Types and Type Annotations](./lesson-03-basic-types-and-type-annotations)
- [Lesson 04: Functions and Type Inference](./lesson-04-functions-and-type-inference)
- [Lesson 05: Objects, Interfaces, and Optional Properties](./lesson-05-objects,-interfaces,-and-optional-properties)
- [Lesson 06: Arrays, Tuples, and readonly](./lesson-06-arrays-tuples-and-readonly)
- [Lesson 07: Union, Intersection, and Literal Types](./lesson-07-union-intersection-and-literal-types)
- [Lesson 08: Type Aliases vs Interfaces](./lesson-08-type-aliases-vs-interfaces)

</div>

</div>

<div class="guru-main" markdown="1">

## What is a Type Alias?

A **type alias** gives a name to any type:

```ts
type UserID = string;
type Status = "active" | "inactive";

type Product = {
  id: number;
  name: string;
};
```

You can use `type` for primitives, unions, intersections, and functions.

---

## What is an Interface?

An **interface** describes the structure of an object:

```ts
interface User {
  id: number;
  name: string;
}
```

Interfaces are extendable and composable, ideal for object shapes and class contracts.

---

## Key Differences

| Feature                  | `type`                                | `interface`                      |
|--------------------------|----------------------------------------|----------------------------------|
| Objects                  | ✅                                      | ✅                                |
| Primitives, unions, etc. | ✅ (strings, unions, functions)         | ❌ only objects                  |
| Extendable               | ✅ via intersections (`&`)              | ✅ via `extends`                |
| Declaration merging      | ❌ no                                  | ✅ supported                    |
| Better for classes       | ❌ not ideal                            | ✅ recommended                  |

---

## When to Use `type` vs `interface`

Use `interface` when:
- Defining **object structures**
- Building APIs, classes, or data models
- You benefit from **declaration merging**

Use `type` when:
- Creating **unions**, **tuples**, or function signatures
- Combining multiple types with `|` or `&`
- Aliasing a primitive or non-object structure

---

## Can You Combine Them?

Yes — you can use both together:

```ts
interface Person {
  name: string;
}

type WithAge = Person & { age: number };
```

> You can even use a type inside an interface or vice versa.

---

## Summary

- `type` is more flexible — can alias anything
- `interface` is better for structured, extendable object types
- Use `interface` for long-lived objects and APIs
- Use `type` for complex unions, intersections, and primitives

Next up: **Working with Enums** — the right way to create named constants and semantic values.

</div>
