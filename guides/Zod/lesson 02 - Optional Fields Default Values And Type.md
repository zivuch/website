---
title: Optional Fields, Default Values, and Type Modifiers
menu_order: 2
post_status: publish
post_excerpt: Learn how to make fields optional, add defaults, and handle nullable values.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Basic Guide to Zod
  post_tag:
    - optional
    - default
    - typescript
    - zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Making Fields Optional](#making-fields-optional)
- [Setting Default Values](#setting-default-values)
- [Nullable vs Optional](#nullable-vs-optional)
- [Chaining Modifiers](#chaining-modifiers)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 01: Introduction to Zod and Schema Basics](./lesson-01-introduction-to-zod-and-schema-basics)
- [Lesson 02: Optional Fields, Default Values, and Type Modifiers](./lesson-02-optional-fields-default-values-and-type)
- [Lesson 03: Arrays, Enums, and Literal Types](./lesson-03-arrays-enums-and-literal-types)
- [Lesson 04: Nested Objects and Schema Composition](./lesson-04-nested-objects-and-schema-composition)
- [Lesson 05: Validation Methods, Error Handling, and Utilities](./lesson-05-validation-methods-error-handling-and-utilities)

</div>

</div>

<div class="guru-main" markdown="1">

## Making Fields Optional

In many real-world scenarios, not all fields are required. Zod makes it easy to declare optional fields using `.optional()`:

```ts
import { z } from "zod";

const UserSchema = z.object({
  name: z.string(),
  age: z.number().optional(),
});
```

Now, `age` is not required:

```ts
UserSchema.parse({ name: "Alice" }); // ✅ Valid
UserSchema.parse({ name: "Alice", age: 30 }); // ✅ Valid
UserSchema.parse({ age: 30 }); // ❌ name is required
```

## Setting Default Values

To automatically assign a value when a field is missing, use `.default()`:

```ts
const UserSchema = z.object({
  name: z.string(),
  age: z.number().default(18),
});
```

Now if `age` is omitted, it defaults to `18`:

```ts
UserSchema.parse({ name: "Bob" });
// ➜ { name: 'Bob', age: 18 }
```

> You can also use both `.optional()` and `.default()` together, but `.default()` already implies optional.

## Nullable vs Optional

Zod distinguishes between:

- **optional** → the key may be missing
- **nullable** → the key may exist, but be `null`

```ts
const schema = z.object({
  age: z.number().nullable(),
});

schema.parse({ age: null }); // ✅
schema.parse({}); // ❌ age is required
```

You can combine both:

```ts
z.number().optional().nullable();
```

## Chaining Modifiers

Zod lets you chain modifiers naturally:

```ts
z.string().min(3).max(20).optional();
```

That means:

- The field must be a string
- Minimum length: 3
- Maximum length: 20
- But it's also optional!

## Summary

- Use `.optional()` for non-required fields
- Use `.default()` to assign fallback values
- Use `.nullable()` to accept `null` values
- Combine them for flexible schema design

---

In the next lesson, we'll explore **arrays, enums, and literal types** with Zod.

---

**_ Master the Code, Be the Guru! _**

</div>
