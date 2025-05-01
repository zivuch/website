---
title: Building Reusable Schemas Across Frontend and Backend
menu_order: 12
post_status: publish
post_excerpt: Share and reuse schemas across frontend and backend for consistent validation.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Advanced Guide to Zod
  post_tag:
    - schema reuse
    - shared types
    - frontend-backend sync
    - zod
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Share Schemas?](#why-share-schemas)
- [Project Structure for Shared Schemas](#project-structure-for-shared-schemas)
- [Defining Schemas Once, Using Everywhere](#defining-schemas-once-using-everywhere)
- [Example: User Registration](#example-user-registration)
- [Tips for Schema Versioning](#tips-for-schema-versioning)
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

## Why Share Schemas?

Imagine this:
- Your **backend** validates request bodies before saving to the database
- Your **frontend** validates user input before sending requests
- Both use **the same logic** — but you’ve written it twice 😰

With Zod, you can define a schema **once**, then reuse it across:
- API endpoints
- Forms and inputs
- TypeScript types
- Testing

> One schema to rule them all.

---

## Project Structure for Shared Schemas

In a monorepo or fullstack project, organize your shared logic like this:

```
/packages
  /schemas
    user.ts
/frontend
/backend
```

Or in a single repo:

```
/src
  /schemas
    user.ts
  /frontend
  /backend
```

Your schema files become single sources of truth.

---

## Defining Schemas Once, Using Everywhere

Let’s define a reusable user schema:

```ts
// src/schemas/user.ts
import { z } from "zod";

export const RegisterSchema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
  password: z.string().min(6),
});

export type RegisterInput = z.infer<typeof RegisterSchema>;
```

Then in your backend route:

```ts
// backend/api/register.ts
import { RegisterSchema } from "@/schemas/user";

const body = await req.json();
const result = RegisterSchema.safeParse(body);
```

And in your frontend form:

```ts
// frontend/forms/RegisterForm.ts
import { RegisterSchema } from "@/schemas/user";

RegisterSchema.parse(formData); // Client-side check
```

---

## Example: User Registration

**Shared schema file:**

```ts
// schemas/user.ts
export const UserLoginSchema = z.object({
  email: z.string().email(),
  password: z.string().min(6),
});

export type UserLoginData = z.infer<typeof UserLoginSchema>;
```

**Backend:**

```ts
const data = await req.json();
const result = UserLoginSchema.safeParse(data);
```

**Frontend:**

```ts
const errors = validateForm(formState, UserLoginSchema);
```

Now both sides stay in sync — no drift, no surprises.

---

## Tips for Schema Versioning

- ✅ Tag your schemas with comments (or filenames) when API versions change
- ✅ Avoid breaking schema changes without tracking them in version control
- ✅ Use `extend()`, `pick()`, and `omit()` to adapt base schemas safely

---

## Summary

- Use Zod to centralize validation logic and types
- Structure your project to share schemas across layers
- Infer types from schemas instead of duplicating interfaces
- Simplify testing, reduce bugs, and save time

---

You’ve reached the end of the **Advanced Guide to Zod**!

Up next: the final section — **Practical Examples, Problems, and Real-World Solutions**.

---

*** Master the Code, Be the Guru! ***

</div>
