---
title: Objects, Interfaces, and Optional Properties
menu_order: 5
post_status: publish
post_excerpt: Learn how to type objects using interfaces, add optional and readonly properties, and build consistent object structures.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - interfaces
    - object typing
    - optional properties
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Typing Objects with Inline Annotations](#typing-objects-with-inline-annotations)
- [Using Interfaces](#using-interfaces)
- [Optional and Readonly Properties](#optional-and-readonly-properties)
- [Extending Interfaces](#extending-interfaces)
- [Type Aliases vs Interfaces for Objects](#type-aliases-vs-interfaces-for-objects)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 01: What is TypeScript and Why Use It](./lesson-01-what-is-typescript-and-why-use-it)
- [Lesson 02: Setting Up TypeScript in Your Project](./lesson-02-setting-up-typescript-in-your-project)
- [Lesson 03: Basic Types and Type Annotations](./lesson-03-basic-types-and-type-annotations)
- [Lesson 04: Functions and Type Inference](./lesson-04-functions-and-type-inference)
- [Lesson 05: Objects, Interfaces, and Optional Properties](./lesson-05-objects,-interfaces,-and-optional-properties)

</div>

</div>

<div class="guru-main" markdown="1">

## Typing Objects with Inline Annotations

You can annotate objects directly:

```ts
const user: {
  name: string;
  age: number;
} = {
  name: "Alex",
  age: 30,
};
```

This works but becomes hard to reuse. Enter interfaces.

---

## Using Interfaces

Use `interface` to define reusable object shapes:

```ts
interface User {
  name: string;
  age: number;
}

const user: User = {
  name: "Lior",
  age: 28,
};
```

Interfaces help maintain consistency across components, APIs, and models.

---

## Optional and Readonly Properties

### Optional `?`

```ts
interface Product {
  id: number;
  description?: string;
}
```

This allows `description` to be omitted.

### Readonly

```ts
interface Config {
  readonly apiKey: string;
}
```

Trying to change `apiKey` after initialization will throw an error during development.

---

## Extending Interfaces

Interfaces can extend each other like classes:

```ts
interface Person {
  name: string;
}

interface Employee extends Person {
  role: string;
}

const e: Employee = {
  name: "Dana",
  role: "Developer",
};
```

This promotes DRY code and composability.

---

## Type Aliases vs Interfaces for Objects

You can also use `type`:

```ts
type Car = {
  brand: string;
  year: number;
};
```

> Prefer `interface` when defining object shapes.  
> Prefer `type` when composing unions, primitives, functions, etc.

Interfaces can be merged (declaration merging), while types are static.

---

## Summary

- Use `interface` to define structured and reusable object types
- Use `?` for optional and `readonly` to prevent mutation
- Extend interfaces to create hierarchical data models
- Know when to use `type` vs `interface` — both are powerful tools

Next up: **arrays, tuples, and how to create safe, structured collections in TypeScript.**

</div>
