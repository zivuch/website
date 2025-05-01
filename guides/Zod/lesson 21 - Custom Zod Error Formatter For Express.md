---
title: Bonus – Custom Zod Error Formatter for Express APIs
menu_order: 22
post_status: publish
post_excerpt: Format Zod errors for consistent API responses using a custom Express handler.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Practical Guide to Zod
  post_tag:
    - error formatting
    - express
    - api design
    - zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Format Zod Errors?](#why-format-zod-errors)
- [What a Good API Error Response Looks Like](#what-a-good-api-error-response-looks-like)
- [Creating a Zod Error Formatter](#creating-a-zod-error-formatter)
- [Using It in Middleware](#using-it-in-middleware)
- [Optional: Global Express Error Handler](#optional-global-express-error-handler)
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

## Why Format Zod Errors?

By default, Zod gives you a rich error object. But clients often expect:

- A clean structure
- Flat key-value errors
- Easy-to-display messages in forms or frontend UIs

Instead of returning raw `.issues`, let’s format errors into something like:

```json
{
  "errors": {
    "email": "Invalid email",
    "password": "Too short"
  }
}
```

---

## What a Good API Error Response Looks Like

Here’s a simple, predictable structure:

```json
{
  "status": "error",
  "message": "Validation failed",
  "errors": {
    "field": "Error message"
  }
}
```

Let’s build a utility to do that.

---

## Creating a Zod Error Formatter

```ts
import { ZodError } from "zod";

export function formatZodError(error: ZodError) {
  const formatted: Record<string, string> = {};

  for (const issue of error.issues) {
    const path = issue.path.join(".");
    if (!formatted[path]) {
      formatted[path] = issue.message;
    }
  }

  return {
    status: "error",
    message: "Validation failed",
    errors: formatted,
  };
}
```

This gives you a clean, flat object ready to send to any client.

---

## Using It in Middleware

Update your validation middleware to use it:

```ts
import { formatZodError } from "@/utils/formatZodError";

export const validate =
  <T>(schema: ZodSchema<T>) =>
  (req: Request, res: Response, next: NextFunction) => {
    const result = schema.safeParse(req.body);
    if (!result.success) {
      return res.status(400).json(formatZodError(result.error));
    }
    req.body = result.data;
    next();
  };
```

---

## Optional: Global Express Error Handler

For apps with multiple validation points or thrown errors:

```ts
app.use((err, req, res, next) => {
  if (err instanceof ZodError) {
    return res.status(400).json(formatZodError(err));
  }

  console.error(err);
  res.status(500).json({ status: "error", message: "Internal Server Error" });
});
```

---

## Summary

- Use a consistent structure for API validation errors
- Build a reusable `formatZodError()` utility
- Integrate it into middleware or global error handlers
- Clients love predictable error formats — your future self will too

---

*** Master the Code, Be the Guru! ***

</div>
