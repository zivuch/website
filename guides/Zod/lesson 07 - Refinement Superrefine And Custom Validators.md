---
title: Refinement, superRefine, and Custom Validators
menu_order: 7
post_status: publish
post_excerpt: Add custom validation logic with refine and cross-field checks using superRefine.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Advanced Guide to Zod
  post_tag:
    - refine
    - superRefine
    - custom validation
    - advanced zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Use Refinement?](#why-use-refinement)
- [Using refine() for Single-Field Logic](#using-refine-for-single-field-logic)
- [Using superRefine() for Cross-Field Logic](#using-superrefine-for-cross-field-logic)
- [Adding Custom Error Messages](#adding-custom-error-messages)
- [Practical Use Case: Confirm Password](#practical-use-case-confirm-password)
- [Summary](#summary)

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

</div>

<div class="guru-main" markdown="1">

## Why Use Refinement?

Zod is great at validating **types** — but sometimes you need more:

- Is a number even?
- Does a string contain uppercase letters?
- Do two fields match?

That’s where `.refine()` and `.superRefine()` come in.

---

## Using `refine()` for Single-Field Logic

`refine()` adds custom logic to a **single field**:

```ts
const PasswordSchema = z
  .string()
  .min(6)
  .refine((val) => /[A-Z]/.test(val), {
    message: "Password must include at least one uppercase letter",
  });
```

If the value passes the `.min(6)` check but not the uppercase test, the custom error will be shown.

---

## Using `superRefine()` for Cross-Field Logic

Need to compare two or more fields? Use `.superRefine()` on `z.object()`:

```ts
const RegisterSchema = z
  .object({
    password: z.string(),
    confirmPassword: z.string(),
  })
  .superRefine((data, ctx) => {
    if (data.password !== data.confirmPassword) {
      ctx.addIssue({
        path: ["confirmPassword"],
        code: z.ZodIssueCode.custom,
        message: "Passwords do not match",
      });
    }
  });
```

- `ctx.addIssue()` lets you precisely control **which field** the error appears on.
- The `path` is optional but useful for forms and UI feedback.

---

## Adding Custom Error Messages

You can add messages to almost any Zod method:

```ts
z.string().min(3, { message: "Too short" });
z.number().positive({ message: "Must be a positive number" });
```

This makes validation much more user-friendly and localizable.

---

## Practical Use Case: Confirm Password

Let’s combine everything:

```ts
const ConfirmPasswordSchema = z
  .object({
    password: z.string().min(6),
    confirmPassword: z.string(),
  })
  .superRefine(({ password, confirmPassword }, ctx) => {
    if (password !== confirmPassword) {
      ctx.addIssue({
        code: "custom",
        path: ["confirmPassword"],
        message: "Passwords must match",
      });
    }
  });
```

Now you can validate and give user-friendly error messages with full control.

---

## Summary

- Use `.refine()` for advanced single-field checks
- Use `.superRefine()` for object-level and cross-field logic
- Add custom error messages for better user experience
- Combine them for powerful, real-world validations

Next up: **Lesson 8 – Discriminated Unions and Tagged Types**, a key tool for polymorphic schemas like multi-step forms or API responses.

---

**_ Master the Code, Be the Guru! _**

</div>
