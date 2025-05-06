---
title: Defining API Schemas with Zod and TypeScript
menu_order: 18
post_status: publish
post_excerpt: Learn how to use Zod with TypeScript to validate and type-safe your API inputs, bodies, queries, and responses.
taxonomy:
  category:
    - typescript
    - Practical Guide to TypeScript
  post_tag:
    - typescript
    - zod
    - api validation
    - schema
    - express
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Use Zod with TypeScript](#why-use-zod-with-typescript)
- [Installing Zod](#installing-zod)
- [Creating and Using Schemas](#creating-and-using-schemas)
- [Inferring Types from Zod Schemas](#inferring-types-from-zod-schemas)
- [Validating API Request Data](#validating-api-request-data)
- [Reusable Middleware for Express](#reusable-middleware-for-express)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 16: Using TypeScript in a React Project](./lesson-16-using-typescript-in-a-react-project)
- [Lesson 17: Using TypeScript with Node.js and Express](./lesson-17-using-typescript-with-nodejs-and-express)
- [Lesson 18: Defining API Schemas with Zod and TypeScript](./lesson-18-defining-api-schemas-with-zod-and-typescript)
- [Lesson 19: Integrating TypeScript with Zustand or Redux](./lesson-19-integrating-typescript-with-zustand-or-redux)

</div>

</div>

<div class="guru-main" markdown="1">

## Why Use Zod with TypeScript

Zod is a **TypeScript-first validation library** that lets you:

- Validate data at runtime (like `req.body`)
- Automatically **generate TypeScript types** from schemas
- Reduce duplication between validation and type declarations

Perfect for full-stack TypeScript projects.

---

## Installing Zod

```bash
npm install zod
```

---

## Creating and Using Schemas

```ts
import { z } from "zod";

const UserSchema = z.object({
  name: z.string(),
  age: z.number().min(18)
});
```

Now you can validate and parse input:

```ts
const result = UserSchema.safeParse(req.body);

if (!result.success) {
  return res.status(400).json(result.error);
}

const user = result.data;
```

---

## Inferring Types from Zod Schemas

Use `z.infer<typeof Schema>` to generate matching types:

```ts
type User = z.infer<typeof UserSchema>;

const createUser = (user: User) => {
  // fully typed, matches schema exactly
};
```

This ensures **type and validation are always in sync**.

---

## Validating API Request Data

You can validate:

- `req.body`
- `req.query`
- `req.params`

Example:

```ts
const QuerySchema = z.object({
  page: z.string().regex(/^\d+$/)
});

const queryResult = QuerySchema.safeParse(req.query);
```

---

## Reusable Middleware for Express

Create a custom middleware:

```ts
function validate(schema: z.ZodTypeAny) {
  return (req: Request, res: Response, next: NextFunction) => {
    const result = schema.safeParse(req.body);
    if (!result.success) {
      return res.status(400).json(result.error.flatten());
    }
    req.body = result.data;
    next();
  };
}

// Usage:
app.post("/users", validate(UserSchema), (req, res) => {
  const user = req.body; // now fully typed + validated
  res.status(201).json(user);
});
```

---

## Summary

- Zod is the ideal partner for TypeScript APIs
- Define your schema once — and infer types automatically
- Use `.safeParse()` for clean validation with no exceptions
- Build reusable middleware to keep your Express routes clean

Next up: **Lesson 19 – Integrating TypeScript with Zustand or Redux**

</div>
