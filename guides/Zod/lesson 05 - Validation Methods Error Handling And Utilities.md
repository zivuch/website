---
title: Validation Methods, Error Handling, and Zod Utilities
menu_order: 5
post_status: publish
post_excerpt: Understand parse vs safeParse, and how to handle validation errors effectively.
taxonomy:
  category:
    - zod
    - Basic Guide to Zod
  post_tag:
    - validation
    - error handling
    - utilities
    - parse
    - safeParse
---

<div class="toc" markdown="1">

## On this Page

- [parse() vs safeParse()](#parse-vs-safeparse)
- [Understanding Validation Errors](#understanding-validation-errors)
- [Using refine() for Custom Validation](#using-refine-for-custom-validation)
- [Preprocessing Input Values](#preprocessing-input-values)
- [Type Inference and z.infer](#type-inference-and-zinfer)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## parse() vs safeParse()

You’ve seen both methods before, but let’s compare them clearly:

### `parse()`

- Throws an error if validation fails
- Simple to use for strict data parsing

```ts
const schema = z.string().min(3);
schema.parse("abc"); // ✅
schema.parse("a");   // ❌ throws ZodError
```

### `safeParse()`

- Returns a result object
- Better for production usage and form handling

```ts
const result = schema.safeParse("a");

if (!result.success) {
  console.log(result.error.issues); // ➜ array of issues
}
```

Use `.safeParse()` when you want full control over error handling without throwing exceptions.

## Understanding Validation Errors

Zod gives you detailed error reports:

```ts
const schema = z.object({
  email: z.string().email(),
});

const result = schema.safeParse({ email: "not-an-email" });

if (!result.success) {
  console.log(result.error.format());
}
```

The `.format()` method turns raw errors into a readable nested object structure — great for displaying errors in UI forms.

## Using refine() for Custom Validation

Need to validate logic that isn’t covered by Zod’s built-in checks? Use `.refine()`:

```ts
const PasswordSchema = z.string().min(6).refine(
  (val) => /[A-Z]/.test(val),
  { message: "Must include at least one uppercase letter" }
);
```

You can even access the full object when refining fields inside `z.object()` using `.superRefine()` (we’ll cover that in the advanced guide).

## Preprocessing Input Values

Use `z.preprocess()` to transform data before validation. Example: convert a string to a number:

```ts
const schema = z.preprocess((val) => Number(val), z.number());

schema.parse("42"); // ✅ returns number 42
```

This is helpful when working with form data, query params, or environment variables.

## Type Inference and z.infer

Zod schemas are fully type-safe:

```ts
const UserSchema = z.object({
  name: z.string(),
  age: z.number(),
});

type User = z.infer<typeof UserSchema>;
```

Now, `User` will be:

```ts
// {
//   name: string;
//   age: number;
// }
```

Zod is a single source of truth: no need to repeat your types.

## Summary

- Use `.safeParse()` for safe, non-throwing validation
- Zod errors are structured and easy to format
- Use `.refine()` for custom logic
- Use `.preprocess()` to clean/transform input
- Leverage `z.infer` to sync runtime validation with static types

---

That wraps up the **Basic Guide to Zod**.  
Next, we’ll dive into the **Advanced Guide**, where we cover schema composition, discriminated unions, transforms, and more.

---

*** Master the Code, Be the Guru! ***

</div>
