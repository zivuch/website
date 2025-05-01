---
title: Validating Environment Variables with Zod
menu_order: 15
post_status: publish
post_excerpt: Enforce environment variable structure and fail fast with dotenv + Zod.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Practical Guide to Zod
  post_tag:
    - env validation
    - dotenv
    - configuration
    - zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [The Problem](#the-problem)
- [Zod Schema for Environment Variables](#zod-schema-for-environment-variables)
- [Using with dotenv](#using-with-dotenv)
- [Type Inference and Access](#type-inference-and-access)
- [Fail Fast on Misconfiguration](#fail-fast-on-misconfiguration)
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

Environment variables are prone to errors:
- Missing `DATABASE_URL`
- Typos like `PROT` instead of `PORT`
- Invalid formats like `"true"` instead of a boolean

Let’s fix that by validating `process.env` at startup using Zod.

---

## Zod Schema for Environment Variables

```ts
import { z } from "zod";

export const EnvSchema = z.object({
  NODE_ENV: z.enum(["development", "production", "test"]),
  PORT: z
    .string()
    .default("3000")
    .transform((val) => parseInt(val, 10)),
  DATABASE_URL: z.string().url(),
  ENABLE_CACHE: z
    .string()
    .optional()
    .transform((val) => val === "true"),
});
```

We validate and **convert** values as needed (e.g. string → number or boolean).

---

## Using with `dotenv`

```ts
import dotenv from "dotenv";
dotenv.config(); // Load .env into process.env

const result = EnvSchema.safeParse(process.env);

if (!result.success) {
  console.error("❌ Invalid environment configuration:", result.error.format());
  process.exit(1); // Fail fast
}

export const env = result.data;
```

Now you can import `env` anywhere in your app with confidence.

---

## Type Inference and Access

```ts
console.log(env.PORT); // number
console.log(env.ENABLE_CACHE); // boolean
```

By using `transform()`, the types are **inferred automatically**.

---

## Fail Fast on Misconfiguration

This pattern helps you:
- Catch errors at startup
- Avoid runtime crashes due to undefined or wrong values
- Keep `.env.example` accurate and enforced

---

## Summary

- Use Zod to validate `process.env` and apply default values
- Use `.transform()` to coerce strings to proper types
- Integrate with `dotenv` and fail fast on config issues
- Export the validated `env` object to use app-wide

---

Next: **Lesson 16 – Handling Nested Errors and Formatted Output with Zod**

---

*** Master the Code, Be the Guru! ***

</div>
