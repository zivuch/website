---
title: Arrays Tuples and readonly
menu_order: 6
post_status: publish
post_excerpt: Learn how to type arrays, work with tuples, and enforce immutability using readonly in TypeScript.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - arrays
    - tuples
    - readonly
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Typing Arrays](#typing-arrays)
- [Readonly Arrays](#readonly-arrays)
- [Tuples in TypeScript](#tuples-in-typescript)
- [Labeled Tuples](#labeled-tuples)
- [When to Use Tuples vs Arrays](#when-to-use-tuples-vs-arrays)
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

</div>

</div>

<div class="guru-main" markdown="1">

## Typing Arrays

You can type arrays in two ways:

```ts
let numbers: number[] = [1, 2, 3];
let fruits: Array<string> = ["apple", "banana"];
```

Both are valid. Choose whichever is more readable in your context.

---

## Readonly Arrays

To prevent mutation of an array:

```ts
const values: readonly number[] = [1, 2, 3];
```

Now methods like `.push()` or `.splice()` will trigger type errors.

```ts
values.push(4); // ❌ Error
```

You can also use:

```ts
const colors: ReadonlyArray<string> = ["red", "blue"];
```

---

## Tuples in TypeScript

Tuples are fixed-length arrays with fixed types:

```ts
let person: [string, number] = ["Alice", 30];
```

Each index has a known type. Tuples are useful when:
- The **length is known**
- The **order matters**
- Each element has a **distinct meaning**

---

## Labeled Tuples

You can label tuple elements for better clarity (editor-only feature):

```ts
type Point = [x: number, y: number];

const p: Point = [10, 20];
```

> It doesn't affect runtime, but improves readability and tooling.

---

## When to Use Tuples vs Arrays

| Use Case            | Recommendation      |
|---------------------|---------------------|
| Homogeneous list     | Use `type[]` or `Array<type>` |
| Fixed-length record | Use `tuple`         |
| Mixed types         | Use `tuple`         |
| Immutable list      | Add `readonly`      |

---

## Summary

- Arrays hold values of the same type; tuples hold fixed, typed positions
- Use `readonly` or `ReadonlyArray<T>` to enforce immutability
- Tuples are ideal when data has a known structure with position-based meaning

Coming up: **union types, intersection types, and how to combine types powerfully in TypeScript.**

</div>
