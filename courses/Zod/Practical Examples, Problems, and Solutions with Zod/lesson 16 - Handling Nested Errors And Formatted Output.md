---
title: Handling Nested Errors and Formatted Output with Zod
menu_order: 16
post_status: publish
taxonomy:
  category:
    - zod
  post_tag:
    - error handling
    - validation
    - safeParse
    - flatten
    - form feedback
---

<div class="toc" markdown="1">

## On this Page

- [The Problem](#the-problem)
- [Nested Validation Errors](#nested-validation-errors)
- [Using error.format()](#using-errorformat)
- [Flattening Errors for Form Inputs](#flattening-errors-for-form-inputs)
- [Custom Error Paths](#custom-error-paths)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## The Problem

When validating complex objects like:

```ts
const schema = z.object({
  user: z.object({
    name: z.string().min(2),
    email: z.string().email(),
  }),
});
```

You want to **surface meaningful error messages** for nested fields like:
- `user.name`
- `user.email`

But raw Zod errors can be verbose. Let’s fix that.

---

## Nested Validation Errors

```ts
const result = schema.safeParse({
  user: {
    name: "",
    email: "not-an-email",
  },
});
```

If validation fails, the result is:

```ts
{
  success: false,
  error: ZodError
}
```

---

## Using `error.format()`

Zod provides a great method to **structure errors** by field:

```ts
if (!result.success) {
  console.log(result.error.format());
}
```

This returns a **tree-like object**:

```ts
{
  user: {
    name: { _errors: ["String must contain at least 2 characters"] },
    email: { _errors: ["Invalid email"] }
  },
  _errors: []
}
```

Perfect for building inline form error messages.

---

## Flattening Errors for Form Inputs

You can also flatten all errors into a simpler format:

```ts
const flat = result.error.flatten();

console.log(flat.fieldErrors);
// ➜ {
//   "user.name": undefined,
//   "user.email": ["Invalid email"]
// }
```

> Note: `flatten()` works best on flat schemas. For deeply nested ones, use `.format()` instead.

---

## Custom Error Paths

If you're using `.superRefine()` or `.addIssue()`, you can control which field gets the error:

```ts
ctx.addIssue({
  path: ["user", "email"],
  code: z.ZodIssueCode.custom,
  message: "This email already exists",
});
```

This ensures the error appears exactly where you want it.

---

## Summary

- Use `.format()` to get a structured object of errors per field
- Use `.flatten()` to get a simple key-value structure
- Use `path` in `.addIssue()` for accurate error targeting
- Zod makes it easy to wire backend errors into frontend UIs

---

Next: **Lesson 17 – Creating a Reusable Zod Error Parser for Forms**

---

*** Master the Code, Be the Guru! ***

</div>
