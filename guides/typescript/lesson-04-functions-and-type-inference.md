---
title: Functions and Type Inference
menu_order: 4
post_status: publish
post_excerpt: Learn how to define functions in TypeScript with typed parameters, return types, and automatic type inference.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - functions
    - type inference
    - parameters
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Function Parameters and Return Types](#function-parameters-and-return-types)
- [Type Inference in Functions](#type-inference-in-functions)
- [Optional and Default Parameters](#optional-and-default-parameters)
- [Arrow Functions and Typing](#arrow-functions-and-typing)
- [Function Types as Variables](#function-types-as-variables)
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

## Function Parameters and Return Types

You can type both parameters and return values:

```ts
function add(x: number, y: number): number {
  return x + y;
}
```

This ensures the function always receives and returns the correct types.

---

## Type Inference in Functions

TypeScript can infer the return type:

```ts
function greet(name: string) {
  return `Hello, ${name}`;
}
```

But for public APIs or exports, it’s best to **explicitly define** return types for clarity and safety.

---

## Optional and Default Parameters

### Optional parameter

```ts
function log(message: string, user?: string) {
  console.log(`${message}${user ? " from " + user : ""}`);
}
```

### Default parameter

```ts
function multiply(a: number, b: number = 2): number {
  return a * b;
}
```

---

## Arrow Functions and Typing

Arrow functions can be typed like this:

```ts
const subtract = (a: number, b: number): number => a - b;
```

You can also define the function type separately:

```ts
const divide: (a: number, b: number) => number = (a, b) => a / b;
```

---

## Function Types as Variables

You can define reusable function signatures:

```ts
type MathOperation = (a: number, b: number) => number;

const add: MathOperation = (a, b) => a + b;
const sub: MathOperation = (a, b) => a - b;
```

This is especially helpful for callbacks or utilities passed between components.

---

## Summary

- Type parameters and return values explicitly for safety and clarity
- TypeScript can infer return types but prefer annotations for public APIs
- Use `?` for optional parameters and `=` for default values
- Arrow functions can also be typed cleanly using type aliases

Up next: **how to define objects and interfaces with optional, readonly, and structured properties**.

</div>
