---
title: Creating a Reusable Zod Error Parser for Forms
menu_order: 17
post_status: publish
post_excerpt: Build a reusable Zod error parser to simplify form handling in React.
taxonomy:
  category:
    - zod
    - Practical Guide
  post_tag:
    - form validation
    - error formatting
    - reusable utility
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [Why Create a Reusable Error Parser?](#why-create-a-reusable-error-parser)
- [Building the parseZodErrors Utility](#building-the-parsezoderrors-utility)
- [Using It in React Forms](#using-it-in-react-forms)
- [Advanced: Handling Nested Keys](#advanced-handling-nested-keys)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Create a Reusable Error Parser?

Zod gives great error information — but every form needs:
- A way to map Zod errors to individual inputs
- A flat structure like: `{ email: "Invalid", password: "Too short" }`

Rather than rewrite this logic every time, let’s centralize it 💡

---

## Building the `parseZodErrors` Utility

```ts
import { ZodError } from "zod";

export function parseZodErrors(error: ZodError) {
  const formatted: Record<string, string> = {};
  const issues = error.issues;

  for (const issue of issues) {
    const path = issue.path.join(".");
    if (!formatted[path]) {
      formatted[path] = issue.message;
    }
  }

  return formatted;
}
```

### Example Output:

```ts
{
  "email": "Invalid email address",
  "password": "Password must be at least 6 characters"
}
```

---

## Using It in React Forms

```ts
import { parseZodErrors } from "@/utils/parseZodErrors";

const result = RegisterSchema.safeParse(formValues);

if (!result.success) {
  const fieldErrors = parseZodErrors(result.error);

  setFormErrors(fieldErrors);
}
```

Now your form can easily display:

```tsx
{errors.email && <p>{errors.email}</p>}
```

---

## Advanced: Handling Nested Keys

For nested forms, you'll still get dotted keys like `user.email`. You can:
- Leave them as-is for libraries like React Hook Form (supports dot notation)
- Or split them manually for deeply nested custom UIs

```ts
fieldErrors["user.email"]; // works if your form inputs use dot notation
```

> Bonus: You could extend `parseZodErrors` to support nested objects too, if your UI needs that.

---

## Summary

- Centralize Zod error formatting in a reusable helper
- Map errors to form fields with `issue.path.join(".")`
- Works with any schema, flat or nested
- Makes frontend integration clean and repeatable

---

Next: **Lesson 18 – Real-World Case Study: Validating a Blog Post Editor**

---

*** Master the Code, Be the Guru! ***

</div>
