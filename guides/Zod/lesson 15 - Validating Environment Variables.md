---
title: Validating Environment Variables with Zod
menu_order: 15
post_status: publish
post_excerpt: Enforce environment variable structure and fail fast with dotenv + Zod.
taxonomy:
  category:
    - zod
    - Practical Guide
  post_tag:
    - env validation
    - dotenv
    - configuration
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [The Problem](#the-problem)
- [Zod Schema for Environment Variables](#zod-schema-for-environment-variables)
- [Using with dotenv](#using-with-dotenv)
- [Type Inference and Access](#type-inference-and-access)
- [Fail Fast on Misconfiguration](#fail-fast-on-misconfiguration)
- [Summary](#summary)

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
