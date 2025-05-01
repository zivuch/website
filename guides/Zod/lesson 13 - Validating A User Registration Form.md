---
title: Validating a User Registration Form
menu_order: 13
post_status: publish
post_excerpt: Validate complex registration forms with confirm password and business rules.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Practical Guide to Zod
  post_tag:
    - form validation
    - registration
    - real-world
    - zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [The Problem](#the-problem)
- [Zod Schema for Registration](#zod-schema-for-registration)
- [Validating Password Confirmation](#validating-password-confirmation)
- [Handling and Displaying Errors](#handling-and-displaying-errors)
- [Summary](#summary)

</div>

</div>

<div class="otg" markdown="1">

## On this Guide
- [Lesson 13: Validating a User Registration Form](./lesson-13-validating-a-user-registration-form)
- [Lesson 14: Validating API Query Parameters](./lesson14-validating-api-query-parameters)
- [Lesson 15: Validating Environment Variables](./lesson-15-validating-environment-variables)
- [Lesson 16: Handling Nested Errors and Formatted Output](./lesson-16-handling-nested-errors-and-formatted-output)
- [Lesson 17: Reusable Zod Error Parser for Forms](./lesson-17-reusable-zod-error-parser-for-forms)
- [Lesson 18: Blog Post Editor – Real-World Case Study](./lesson-18-blog-post-editor-real-world-case)
- [Lesson 19: Zod + React Hook Form Integration](./lesson-19-zod-react-hook-form-integration)
- [Lesson 21: Validating Express Requests with Zod](./lesson20-validating-express-requests-with-zod)
- [Lesson 22: Custom Zod Error Formatter for Express APIs](./lesson-21-custom-zod-error-formatter-for-express)
- [Lesson 20: Final Thoughts, Best Practices, and Resources](./lesson-22-final-thoughts-best-practices-and-resources)

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
