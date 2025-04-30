---
title: Introduction to Zod and Schema Basics
menu_order: 1
post_status: publish
post_excerpt: A beginner-friendly introduction to Zod, schemas, and basic parsing.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Basic Guide to Zod
  post_tag:
    - typescript
    - validation
    - schema
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [What is Zod?](#what-is-zod)
- [Why Use Zod?](#why-use-zod)
- [Installing Zod](#installing-zod)
- [Creating Your First Schema](#creating-your-first-schema)
- [Parsing and Validating Data](#parsing-and-validating-data)
- [Type Inference](#type-inference)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## What is Zod? <a id="what-is-zod"></a>

**Zod** is a TypeScript-first schema declaration and validation library. It lets you define the **shape of your data** in code and then **validate** incoming data (like API responses, form inputs, environment variables, etc.) at runtime - all while providing **type safety**.

## Why Use Zod?

- Zero dependencies
- Fully TypeScript-native (no need to maintain separate type definitions)
- Runtime validation and static typing combined
- Clean and fluent API
- Replaces verbose and fragile `typeof` or manual validation code

> If you’ve ever used Yup or Joi, Zod plays a similar role - but with better TypeScript support.

## Installing Zod

You can install Zod using npm or yarn:

```bash
npm install zod
# or
yarn add zod
```

No need for extra TypeScript types - it’s already TypeScript-native out of the box.

## Creating Your First Schema

Let’s define a simple schema for a user:

```ts
import { z } from "zod";

const UserSchema = z.object({
  name: z.string(),
  age: z.number(),
});
```

This creates a schema that expects an object with:
- `name`: a string
- `age`: a number

> You just defined both a runtime validator and a TypeScript type in one place!

## Parsing and Validating Data

Zod provides two ways to validate data:

### `.parse()`

Throws an error if the data is invalid:

```ts
UserSchema.parse({ name: "Alice", age: 30 }); // ✅ OK

UserSchema.parse({ name: "Bob" }); // ❌ Throws: age is required
```

### `.safeParse()`

Returns a result object without throwing:

```ts
const result = UserSchema.safeParse({ name: "Alice", age: 30 });

if (result.success) {
  console.log("Valid data:", result.data);
} else {
  console.error("Validation errors:", result.error.issues);
}
```

This method is better for form validation and error handling in production.

## Type Inference

Zod can infer the TypeScript type from your schema:

```ts
type User = z.infer<typeof UserSchema>;

// Now `User` is:
/// {
///   name: string;
///   age: number;
/// }
```

This avoids redundant type declarations and keeps your types and runtime logic in sync.

## Summary

- Zod helps define and validate data shapes with full TypeScript support
- Use `.parse()` for quick checks, and `.safeParse()` for safer error handling
- Infer types from your schemas with `z.infer`

---

Next lesson, we’ll cover **optional fields, default values**, and **basic type modifiers**.

---

*** Master the Code, Be the Guru! ***

</div>
