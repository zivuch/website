---
title: Schema Composition with Merge, Extend, Pick, and Omit
menu_order: 6
post_status: publish
post_excerpt: Master schema composition using merge, extend, pick, and omit.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Advanced Guide to Zod
  post_tag:
    - schema composition
    - extend
    - merge
    - pick
    - omit
---

<div class="toc" markdown="1">

## On this Page

- [Why Schema Composition Matters](#why-schema-composition-matters)
- [Merging Schemas with merge()](#merging-schemas-with-merge)
- [Adding Fields with extend()](#adding-fields-with-extend)
- [Selecting Fields with pick()](#selecting-fields-with-pick)
- [Removing Fields with omit()](#removing-fields-with-omit)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Schema Composition Matters

In real-world projects, you often reuse and reshape your schemas:
- Share a base schema across multiple variations
- Exclude fields before exposing them in the frontend
- Split logic between database, form validation, and API

Zod provides several helpful tools for this: `merge()`, `extend()`, `pick()`, and `omit()`.

---

## Merging Schemas with `merge()`

Combines two schemas of type `z.object()` into one:

```ts
const Base = z.object({ id: z.string() });
const Profile = z.object({ name: z.string() });

const User = Base.merge(Profile);
```

The result:

```ts
User.parse({ id: "123", name: "Alice" }); // ✅
```

> ⚠️ Note: Conflicts will favor the second schema (`Profile` in this case).

---

## Adding Fields with `extend()`

Use `extend()` to add more fields to an existing schema:

```ts
const User = z.object({ name: z.string() });

const Admin = User.extend({
  role: z.literal("admin"),
});
```

This preserves the original schema and creates a new one with additional fields.

---

## Selecting Fields with `pick()`

If you only want part of a schema (e.g. just `id` and `email`), use `pick()`:

```ts
const FullUser = z.object({
  id: z.string(),
  name: z.string(),
  email: z.string(),
});

const PublicUser = FullUser.pick({ id: true, email: true });
```

Now `PublicUser` only accepts `{ id, email }`.

---

## Removing Fields with `omit()`

The opposite of `pick()`. Remove sensitive/internal fields like passwords:

```ts
const DBUser = z.object({
  id: z.string(),
  email: z.string(),
  password: z.string(),
});

const SafeUser = DBUser.omit({ password: true });
```

`SafeUser` no longer allows `password` to appear.

---

## Summary

- Use `.merge()` to combine schemas
- Use `.extend()` to add fields cleanly
- Use `.pick()` and `.omit()` to reshape schemas for different use cases

Next up: **Lesson 7 – Refinement, superRefine, and Custom Validators** for powerful validation logic beyond types.

---

*** Master the Code, Be the Guru! ***

</div>
