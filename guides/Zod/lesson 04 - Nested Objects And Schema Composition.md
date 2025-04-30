---
title: Nested Objects and Schema Composition in Zod
menu_order: 4
post_status: publish
post_excerpt: Nest schemas and reuse them cleanly with extend and merge techniques.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Basic Guide to Zod
  post_tag:
    - nested objects
    - schema composition
    - typescript
    - validation
---

<div class="toc" markdown="1">

## On this Page

- [Nested Object Schemas](#nested-object-schemas)
- [Reusing Schemas](#reusing-schemas)
- [Merging Schemas](#merging-schemas)
- [Extending Schemas](#extending-schemas)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Nested Object Schemas

Zod allows you to nest schemas inside each other, just like you would nest objects in real-world data:

```ts
const AddressSchema = z.object({
  city: z.string(),
  zip: z.string(),
});

const UserSchema = z.object({
  name: z.string(),
  address: AddressSchema,
});
```

Now, the `address` field itself must match the structure defined by `AddressSchema`.

```ts
UserSchema.parse({
  name: "Alice",
  address: { city: "Tel Aviv", zip: "12345" },
}); // ✅
```

Invalid example:

```ts
UserSchema.parse({
  name: "Alice",
  address: { city: "Tel Aviv" },
}); // ❌ zip is missing
```

## Reusing Schemas

Zod encourages reuse. You can define reusable blocks like this:

```ts
const CoordinatesSchema = z.object({
  lat: z.number(),
  lng: z.number(),
});

const PlaceSchema = z.object({
  name: z.string(),
  coords: CoordinatesSchema,
});
```

You write it once, and use it wherever it's needed.

## Merging Schemas

Want to combine two schemas? Use `.merge()`:

```ts
const BaseUser = z.object({
  id: z.string(),
});

const Profile = z.object({
  name: z.string(),
  age: z.number(),
});

const FullUser = BaseUser.merge(Profile);
```

This will create a schema with all the fields from both `BaseUser` and `Profile`.

```ts
FullUser.parse({
  id: "u123",
  name: "Ziv",
  age: 57,
}); // ✅
```

## Extending Schemas

For a more semantic approach, you can use `.extend()` — especially helpful when adding fields:

```ts
const UserSchema = z.object({
  name: z.string(),
});

const AdminSchema = UserSchema.extend({
  role: z.literal("admin"),
});
```

This is perfect for modeling roles, variations, or user permissions.

## Summary

- Nest schemas using `z.object()` inside other objects
- Reuse schema definitions across your app for consistency
- Use `.merge()` to combine multiple schemas
- Use `.extend()` to add more fields while preserving the base

---

Next up, we’ll wrap up the basics with **Lesson 5: Validation Methods, Error Handling, and Zod Utilities**.

---

*** Master the Code, Be the Guru! ***

</div>
