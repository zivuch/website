---
title: Validating a User Registration Form
menu_order: 13
post_status: publish
taxonomy:
  category:
    - zod
  post_tag:
    - form validation
    - registration
    - real-world
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [The Problem](#the-problem)
- [Zod Schema for Registration](#zod-schema-for-registration)
- [Validating Password Confirmation](#validating-password-confirmation)
- [Handling and Displaying Errors](#handling-and-displaying-errors)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## The Problem

We want to validate a **user registration form** with these fields:

- Name (at least 2 characters)
- Email (must be valid)
- Password (at least 6 characters, one uppercase)
- Confirm password (must match password)

We want to:
- Show **helpful error messages**
- Validate on both frontend and backend
- Avoid code duplication

---

## Zod Schema for Registration

```ts
import { z } from "zod";

export const RegisterSchema = z
  .object({
    name: z.string().min(2, "Name must be at least 2 characters"),
    email: z.string().email("Invalid email address"),
    password: z
      .string()
      .min(6, "Password must be at least 6 characters")
      .refine((val) => /[A-Z]/.test(val), {
        message: "Password must contain at least one uppercase letter",
      }),
    confirmPassword: z.string(),
  })
  .superRefine(({ password, confirmPassword }, ctx) => {
    if (password !== confirmPassword) {
      ctx.addIssue({
        path: ["confirmPassword"],
        code: "custom",
        message: "Passwords do not match",
      });
    }
  });
```

---

## Validating Password Confirmation

The `.superRefine()` method is essential for comparing fields. It allows cross-field logic and precise error placement.

```ts
// ❌ Will add error only to confirmPassword
ctx.addIssue({
  path: ["confirmPassword"],
  code: "custom",
  message: "Passwords do not match",
});
```

---

## Handling and Displaying Errors

### In React (e.g. with React Hook Form):

```ts
const result = RegisterSchema.safeParse(formValues);

if (!result.success) {
  const errors = result.error.format();
  console.log(errors.email?._errors); // ["Invalid email address"]
}
```

### In Backend (e.g. Node/Express):

```ts
const body = await request.json();
const result = RegisterSchema.safeParse(body);

if (!result.success) {
  return Response.json({ errors: result.error.flatten() }, { status: 400 });
}
```

---

## Summary

- Zod makes complex form validation clean, readable, and reusable
- Use `.refine()` for field-specific logic, and `.superRefine()` for cross-field validation
- `.safeParse()` gives structured errors for frontend rendering or backend responses

---

Up next: **Lesson 14 – Validating API Query Parameters**

---

*** Master the Code, Be the Guru! ***

</div>
