---
title: Validating Express Requests with Zod
menu_order: 21
post_status: publish
post_excerpt: Validate Express request bodies and params with a clean Zod middleware setup.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Practical Guide
  post_tag:
    - express
    - api validation
    - middleware
    - request validation
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [Why Use Zod in Express?](#why-use-zod-in-express)
- [Creating a Request Schema](#creating-a-request-schema)
- [Building a Reusable Validation Middleware](#building-a-reusable-validation-middleware)
- [Validating req.body, req.query, and req.params](#validating-reqbody-reqquery-and-reqparams)
- [Using z.infer for Typed Handlers](#using-zinfer-for-typed-handlers)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Use Zod in Express?

Express by default accepts any data in `req.body`, `req.query`, and `req.params` — no validation, no typing.

**Zod fixes that** by:
- Catching malformed requests
- Providing clear error messages
- Ensuring consistent structure
- Letting you infer static types for use in handlers

---

## Creating a Request Schema

```ts
import { z } from "zod";

export const CreateUserSchema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
  age: z.number().min(0),
});

export type CreateUserInput = z.infer<typeof CreateUserSchema>;
```

---

## Building a Reusable Validation Middleware

```ts
import { ZodSchema } from "zod";
import { Request, Response, NextFunction } from "express";

export const validate =
  <T>(schema: ZodSchema<T>) =>
  (req: Request, res: Response, next: NextFunction) => {
    const result = schema.safeParse(req.body);
    if (!result.success) {
      return res.status(400).json({ errors: result.error.format() });
    }
    // Attach validated data
    req.body = result.data;
    next();
  };
```

Now you can plug in any Zod schema with a single line.

---

## Validating `req.body`, `req.query`, and `req.params`

You can create separate schemas:

```ts
const QuerySchema = z.object({
  page: z.string().optional(),
});

const ParamsSchema = z.object({
  userId: z.string().uuid(),
});
```

You could then build a `validateQuery` or `validateParams` variant of the middleware — or combine all three with custom wrappers.

---

## Using `z.infer` for Typed Handlers

When you define the schema:

```ts
export type CreateUserInput = z.infer<typeof CreateUserSchema>;
```

You can now type your route handler:

```ts
app.post("/users", validate(CreateUserSchema), (req, res) => {
  const user: CreateUserInput = req.body;
  // Now `user.name`, `user.email`, etc. are fully typed!
  res.json({ user });
});
```

Cleaner, safer, more maintainable.

---

## Summary

- Use Zod to validate and sanitize incoming request data in Express
- Create a reusable `validate()` middleware to apply schemas to routes
- Validate `req.body`, `req.query`, and `req.params` with separate schemas
- Use `z.infer` to infer types for type-safe controller logic
- Catch bad data early and return consistent errors

---

Want bonus content? In the next optional lesson, we can build a **Zod-powered Error Response Formatter** for cleaner API responses.

---

*** Master the Code, Be the Guru! ***

</div>
