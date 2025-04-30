---
title: Validating API Query Parameters
menu_order: 14
post_status: publish
post_excerpt: Cleanly validate query parameters in Express using Zod transformations.
taxonomy:
  category:
    - zod
    - Practical Guide
  post_tag:
    - query params
    - api validation
    - express
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [The Problem](#the-problem)
- [Creating a Query Schema](#creating-a-query-schema)
- [Using Safe Parsing in Express](#using-safe-parsing-in-express)
- [Handling Optional Parameters](#handling-optional-parameters)
- [Dealing with String Inputs](#dealing-with-string-inputs)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## The Problem

Let’s say we have a route like:

```
GET /search?term=react&page=2&sort=desc
```

We want to:
- Validate `term` is a non-empty string
- Validate `page` is an optional positive integer
- Validate `sort` is either `asc` or `desc` (default to `asc`)

---

## Creating a Query Schema

```ts
import { z } from "zod";

export const SearchQuerySchema = z.object({
  term: z.string().min(1, "Search term is required"),
  page: z
    .string()
    .optional()
    .transform((val) => (val ? parseInt(val) : 1))
    .refine((val) => !isNaN(val) && val > 0, {
      message: "Page must be a positive number",
    }),
  sort: z.enum(["asc", "desc"]).optional().default("asc"),
});
```

> Note: query strings come in as **strings**, so you often need `.transform()`.

---

## Using Safe Parsing in Express

```ts
app.get("/search", (req, res) => {
  const result = SearchQuerySchema.safeParse(req.query);

  if (!result.success) {
    return res.status(400).json({ errors: result.error.flatten() });
  }

  const { term, page, sort } = result.data;
  res.json({ term, page, sort });
});
```

Clean, typed, and error-safe. You can now guarantee your handler always gets valid input.

---

## Handling Optional Parameters

Zod makes it easy to work with optional values and defaults:

```ts
page: z
  .string()
  .optional()
  .transform((val) => (val ? parseInt(val) : 1))
```

If the `page` parameter is missing, it will default to `1`.

---

## Dealing with String Inputs

Remember: everything in `req.query` is a string or array of strings.

If your schema expects numbers or booleans, **always use `preprocess` or `transform`**:

```ts
const schema = z.object({
  show: z
    .preprocess((val) => val === "true", z.boolean())
});
```

---

## Summary

- Use Zod to safely validate and transform API query parameters
- Remember to parse strings into numbers or booleans when needed
- Use `.safeParse()` for structured error handling in Express or any backend framework
- Optional fields? Use `.optional()` and `.default()` with `.transform()` as needed

---

Next: **Lesson 15 – Validating Environment Variables with Zod**

---

*** Master the Code, Be the Guru! ***

</div>
