---
title: Transforming and Preprocessing Data with Zod
menu_order: 9
post_status: publish
post_excerpt: Transform and sanitize data using transform and preprocess methods.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Advanced Guide to Zod
  post_tag:
    - transform
    - preprocess
    - data sanitization
    - advanced zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Transform or Preprocess?](#why-transform-or-preprocess)
- [Using transform()](#using-transform)
- [Using preprocess()](#using-preprocess)
- [Differences Between transform and preprocess](#differences-between-transform-and-preprocess)
- [Practical Examples](#practical-examples)
- [Summary](#summary)

</div>

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 06: Schema Composition with Merge, Extend, Pick, and Omit](./lesson-06-schema-composition-with-merge-extend-pick)
- [Lesson 07: Refinement, superRefine, and Custom Validators](./lesson-07-refinement-superrefine-and-custom-validators)
- [Lesson 08: Discriminated Unions and Tagged Types](./lesson-08-discriminated-unions-and-tagged-types)
- [Lesson 09: Transforming and Preprocessing Data](./lesson-09-transforming-and-preprocessing-data)
- [Lesson 10: Working with Records, Maps, Sets, and Enums](./lesson-10-working-with-records-maps-sets-and)
- [Lesson 11: Async Validation with Promises](./lesson-11-async-validation-with-promises)
- [Lesson 12: Reusable Schemas Across Frontend and Backend](./lesson-12-reusable-schemas-across-frontend-and-backend)

</div>

<div class="guru-main" markdown="1">

## Why Transform or Preprocess?

Sometimes raw input isn’t in the shape you want:

- A date string that needs to become a `Date` object
- A number stored as a string
- A string that needs trimming or formatting

Zod offers `.transform()` and `.preprocess()` to fix, convert, or sanitize input during validation.

---

## Using `transform()`

Use `.transform()` **after validation** to shape or derive new values.

```ts
const schema = z.string().transform((val) => val.trim().toUpperCase());

const result = schema.parse("  hello  "); 
// ➜ "HELLO"
```

You can also change the output type:

```ts
const NumSchema = z.string().transform((val) => parseInt(val));

type Result = z.infer<typeof NumSchema>; 
// Result is now `number`, not `string`
```

---

## Using `preprocess()`

Use `.preprocess()` to manipulate values **before** validation happens.

Example: Accept a number or a string and turn it into a number before validating:

```ts
const schema = z.preprocess((val) => Number(val), z.number().min(0));

schema.parse("42"); // ✅ 42
schema.parse(42);   // ✅ 42
schema.parse("abc"); // ❌ Not a number
```

This is great for working with:
- Query strings
- Form data
- Environment variables

---

## Differences Between `transform` and `preprocess`

| Feature         | `.transform()`                     | `.preprocess()`                     |
|----------------|-------------------------------------|-------------------------------------|
| Runs **after** validation | ✅                              | ❌                              |
| Runs **before** validation | ❌                              | ✅                              |
| Can change output type     | ✅                              | ✅                              |
| Use case                   | Reformat/derive                | Sanitize/parse raw input           |

---

## Practical Examples

### 1. Convert date string to `Date` object

```ts
const DateSchema = z
  .string()
  .refine((val) => !isNaN(Date.parse(val)), {
    message: "Invalid date format",
  })
  .transform((val) => new Date(val));
```

### 2. Trim and lowercase email

```ts
const EmailSchema = z
  .string()
  .email()
  .transform((val) => val.trim().toLowerCase());
```

### 3. Parse string to number and validate

```ts
const AgeSchema = z.preprocess(
  (val) => Number(val),
  z.number().int().positive()
);
```

---

## Summary

- Use `.transform()` to clean or reformat values **after validation**
- Use `.preprocess()` to sanitize input **before validation**
- Both are powerful tools to adapt real-world input to strict, type-safe schemas
- Great for working with forms, APIs, and config data

---

Next: **Lesson 10 – Working with Records, Maps, Sets, and Enums in Zod**

---

*** Master the Code, Be the Guru! ***

</div>
