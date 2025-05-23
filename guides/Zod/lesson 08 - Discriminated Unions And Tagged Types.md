---
title: Discriminated Unions and Tagged Types
menu_order: 8
post_status: publish
post_excerpt: Handle multiple schema types with union and discriminatedUnion for clean branching.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Advanced Guide to Zod
  post_tag:
    - union
    - discriminatedUnion
    - tagged types
    - advanced zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What Are Discriminated Unions?](#what-are-discriminated-unions)
- [Creating Unions with z.union()](#creating-unions-with-zunion)
- [Using z.discriminatedUnion()](#using-zdiscriminatedunion)
- [Why Prefer Discriminated Unions](#why-prefer-discriminated-unions)
- [Type Inference and Usage](#type-inference-and-usage)
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

## What Are Discriminated Unions?

A **discriminated union** is a powerful way to define schemas that share some fields, but vary based on a `type` or `kind` field.

Example: Different shapes (`circle`, `square`, `rectangle`) that each require different data.

---

## Creating Unions with `z.union()`

This is the basic way to define multiple schema options:

```ts
const CatSchema = z.object({
  type: z.literal("cat"),
  lives: z.number(),
});

const DogSchema = z.object({
  type: z.literal("dog"),
  breed: z.string(),
});

const PetSchema = z.union([CatSchema, DogSchema]);
```

It works, but it has downsides:

- Harder to infer types
- Manual narrowing needed

---

## Using `z.discriminatedUnion()`

This is the **preferred way** when all options share a common key (like `type`):

```ts
const PetSchema = z.discriminatedUnion("type", [
  z.object({
    type: z.literal("cat"),
    lives: z.number(),
  }),
  z.object({
    type: z.literal("dog"),
    breed: z.string(),
  }),
]);
```

Now Zod:

- Narrows the schema **automatically**
- Produces better TypeScript types
- Validates based on the `type` key

### Example Usage:

```ts
const result = PetSchema.safeParse({
  type: "dog",
  breed: "Golden Retriever",
});

if (result.success) {
  const pet = result.data;

  if (pet.type === "dog") {
    console.log("Breed:", pet.breed);
  }
}
```

No type casting required — Zod does it for you.

---

## Why Prefer Discriminated Unions?

✅ Cleaner syntax  
✅ Easier to maintain  
✅ Stronger TypeScript inference  
✅ Works well for forms, step-based flows, and APIs

---

## Type Inference and Usage

```ts
type Pet = z.infer<typeof PetSchema>;
```

TypeScript will now infer:

```ts
type Pet = { type: "cat"; lives: number } | { type: "dog"; breed: string };
```

Perfect for frontend rendering or backend logic branching.

---

## Summary

- Use `z.union()` for generic union validation
- Use `z.discriminatedUnion()` when your schemas share a `type` or `kind` field
- It simplifies logic, improves inference, and avoids manual narrowing
- Ideal for complex branching data like polymorphic forms and APIs

---

Next up: **Lesson 9 – Transforming and Preprocessing Data with Zod**, where we’ll learn to reshape and sanitize values during validation.

---

**_ Master the Code, Be the Guru! _**

</div>
