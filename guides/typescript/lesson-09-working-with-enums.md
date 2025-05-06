---
title: Working with Enums
menu_order: 9
post_status: publish
post_excerpt: Learn how to define and use enums in TypeScript to create clear, semantic constants with string or numeric values.
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - enums
    - constants
    - semantic types
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is an Enum?](#what-is-an-enum)
- [Numeric Enums](#numeric-enums)
- [String Enums](#string-enums)
- [Reverse Mapping in Enums](#reverse-mapping-in-enums)
- [Enums vs Union Types](#enums-vs-union-types)
- [Best Practices](#best-practices)
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
- [Lesson 09: Working with Enums](./lesson-09-working-with-enums)

</div>

</div>

<div class="guru-main" markdown="1">

## What is an Enum?

An **enum** (short for *enumeration*) is a way to define a **set of named constants**. It helps make your code **more readable and self-documenting**.

---

## Numeric Enums

By default, TypeScript enums are **numeric** and auto-incrementing:

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right
}

const move = Direction.Left; // 2
```

You can override the starting value:

```ts
enum Status {
  Ready = 1,
  Waiting,
  Complete
}
```

Here, `Waiting` becomes 2 and `Complete` becomes 3.

---

## String Enums

String enums are more explicit and readable:

```ts
enum Role {
  Admin = "admin",
  User = "user",
  Guest = "guest"
}

const access = Role.Admin; // "admin"
```

They’re especially useful for API data or UI logic where values must match specific strings.

---

## Reverse Mapping in Enums

Numeric enums support **reverse lookup**:

```ts
enum Color {
  Red,
  Green,
  Blue
}

console.log(Color[1]); // "Green"
```

> 🔒 This doesn’t work with **string enums** (one-way only).

---

## Enums vs Union Types

Consider a union instead of an enum:

```ts
type Direction = "up" | "down" | "left" | "right";
```

### When to prefer enums:
- When using numeric values
- When reverse mapping is needed
- When working with legacy code or class-like structures

### When to prefer union types:
- When using strings and simplicity is preferred
- When working with frontend frameworks or form values

---

## Best Practices

- Prefer **string enums** for clarity
- Avoid `const enum` in code shared with external tools (can break builds)
- Consider `as const` with union types as an alternative:

```ts
const Role = {
  Admin: "admin",
  User: "user"
} as const;

type Role = typeof Role[keyof typeof Role];
```

---

## Summary

- Enums create named constants for better semantics and safety
- Use string enums when readability and exact values matter
- Use union types or `as const` when enums feel too heavy or inflexible

Next up: **Type Assertions and Type Casting** — telling TypeScript exactly what you mean when inference isn’t enough.

</div>
