---
title: Type Assertions and Type Casting
menu_order: 10
post_status: publish
post_excerpt: Learn how to use type assertions in TypeScript to override inferred types and work safely with dynamic data.
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - type assertion
    - type casting
    - unknown types
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is Type Assertion?](#what-is-type-assertion)
- [Using `as` Syntax](#using-as-syntax)
- [When to Use Type Assertions](#when-to-use-type-assertions)
- [Non-null Assertion (`!`)](#non-null-assertion-)
- [Forced Casting with `unknown`](#forced-casting-with-unknown)
- [Avoiding Type Assertion Abuse](#avoiding-type-assertion-abuse)
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
- [Lesson 10: Type Assertions and Type Casting](./lesson-10-type-assertions-and-type-casting)

</div>

</div>

<div class="guru-main" markdown="1">

## What is Type Assertion?

Type assertion tells TypeScript:

> “I know better than you what this type really is.”

It’s used when you **want to override** the compiler’s inferred type.

---

## Using `as` Syntax

The most common form:

```ts
const input = document.getElementById("username") as HTMLInputElement;

console.log(input.value); // Type-safe access to .value
```

You can also use the older angle-bracket syntax:

```ts
const el = <HTMLDivElement>document.querySelector(".box");
```

> ⚠️ Avoid angle brackets in JSX/React files — it conflicts with syntax.

---

## When to Use Type Assertions

Use assertions when:
- Working with **DOM elements**
- Receiving **external data** (e.g., from `JSON.parse`)
- You **know more** than TypeScript’s inference engine

Example:

```ts
const data = '{"name":"Lior"}';
const user = JSON.parse(data) as { name: string };
```

---

## Non-null Assertion (`!`)

If you're sure a value isn't `null` or `undefined`:

```ts
const btn = document.querySelector("button")!;
btn.click();
```

> ⚠️ Dangerous if the element is not guaranteed to exist.

---

## Forced Casting with `unknown`

If a value is `unknown`, you must assert it:

```ts
const val: unknown = "hello";
const len = (val as string).length;
```

For multiple steps, cast through `unknown`:

```ts
const user = "admin" as unknown as boolean;
```

> This is sometimes useful — but also a red flag. Use with care.

---

## Avoiding Type Assertion Abuse

Don't use assertions to **silence errors**:

```ts
// 🚫 Don't do this:
const num = "123" as unknown as number;
```

Use **type guards**, **refinements**, or **safeParse** methods instead.

---

## Summary

- Type assertions override TypeScript’s inference when you’re sure of the type
- Use `as` syntax for DOM, JSON, or dynamic content
- Be cautious with `!` and double-casting — they skip safety
- Use assertions sparingly and intentionally

Next up: **Lesson 11 – Generics in Functions and Interfaces** — the gateway to reusable, type-safe logic.

</div>
