---
title: Union Intersection and Literal Types
menu_order: 7
post_status: publish
post_excerpt: Learn how to combine types in TypeScript using union, intersection, and literal values to model complex logic safely.
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - union types
    - intersection types
    - literal types
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is a Union Type?](#what-is-a-union-type)
- [Literal Types](#literal-types)
- [Type Narrowing with Unions](#type-narrowing-with-unions)
- [What is an Intersection Type?](#what-is-an-intersection-type)
- [Combining Unions and Intersections](#combining-unions-and-intersections)
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

</div>

</div>

<div class="guru-main" markdown="1">

## What is a Union Type?

A **union type** allows a value to be **one of several types**:

```ts
let input: string | number;

input = "hello";
input = 42;
```

Useful when a variable can take on multiple, known types.

---

## Literal Types

**Literal types** are string, number, or boolean values themselves as types:

```ts
type Status = "success" | "error" | "loading";

let state: Status = "success";
```

They’re perfect for enums, flags, and discriminated unions.

---

## Type Narrowing with Unions

TypeScript smartly **narrows** the type based on runtime checks:

```ts
function printLength(value: string | string[]) {
  if (typeof value === "string") {
    return value.length;
  } else {
    return value.join(", ").length;
  }
}
```

This is called **type narrowing** — a core TypeScript feature.

---

## What is an Intersection Type?

An **intersection type** combines multiple types into one:

```ts
type Timestamped = { createdAt: Date };
type User = { name: string };

type TimestampedUser = User & Timestamped;

const user: TimestampedUser = {
  name: "Sam",
  createdAt: new Date(),
};
```

All required fields from both types must be present.

---

## Combining Unions and Intersections

You can build flexible and strict structures:

```ts
type Response =
  | { status: "success"; data: string }
  | { status: "error"; error: string };
```

Or combine behaviors:

```ts
type Loggable = { log: () => void };
type Savable = { save: () => void };

type Logger = Loggable & Savable;
```

---

## Summary

- Use **union types** to allow multiple possible types
- Use **literal types** for specific value constraints
- Use **intersection types** to merge multiple types into one
- Leverage **type narrowing** with `typeof`, `in`, and `instanceof` for safety

Up next: **Type Aliases vs Interfaces** — when to use each and why.

</div>
