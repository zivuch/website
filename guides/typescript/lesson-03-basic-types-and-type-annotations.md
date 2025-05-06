---
title: Basic Types and Type Annotations
menu_order: 3
post_status: publish
post_excerpt: Learn how to declare variables using TypeScript's built-in types string, number, boolean, arrays, and more.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - type annotations
    - static types
    - variables
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What are Type Annotations?](#what-are-type-annotations)
- [Core Primitive Types](#core-primitive-types)
- [Arrays and Tuples](#arrays-and-tuples)
- [Any vs Unknown](#any-vs-unknown)
- [Void, Null, and Undefined](#void-null-and-undefined)
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

## What are Type Annotations?

Type annotations tell TypeScript the **kind of value** a variable will hold.

```ts
let username: string = "Ziv";
let age: number = 30;
let isAdmin: boolean = true;
```

You can declare a type with `:` after the variable name.

---

## Core Primitive Types

### `string`, `number`, `boolean`

```ts
let firstName: string = "Ada";
let score: number = 99.5;
let active: boolean = false;
```

---

## Arrays and Tuples

### Arrays

```ts
let fruits: string[] = ["apple", "banana"];
let scores: number[] = [10, 20, 30];
```

Or using generic notation:

```ts
let values: Array<number> = [1, 2, 3];
```

### Tuples

Tuples are fixed-length arrays with known types:

```ts
let user: [string, number] = ["Alex", 42];
```

---

## Any vs Unknown

### `any` disables type checking:

```ts
let data: any = "Could be anything";
data = 123; // valid
data = true;
```

### `unknown` is safer — must be checked before use:

```ts
let input: unknown = "hello";

if (typeof input === "string") {
  console.log(input.toUpperCase());
}
```

> Prefer `unknown` over `any` for external data when you want safety.

---

## Void, Null, and Undefined

### `void` = no return

```ts
function logMessage(): void {
  console.log("Hello");
}
```

### `null` and `undefined`

You can allow them explicitly:

```ts
let maybe: string | null = null;
let value: number | undefined = undefined;
```

---

## Summary

- Use type annotations to clearly declare value types
- Master core types: `string`, `number`, `boolean`, `array`, `tuple`
- Avoid `any` unless absolutely necessary — prefer `unknown` when unsure
- Understand when to use `void`, `null`, and `undefined`

Next up: **how functions work in TypeScript, with full type inference and safety**.

</div>
