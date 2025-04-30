---
title: Arrays, Enums, and Literal Types in Zod
menu_order: 3
post_status: publish
post_excerpt: Explore array validation, enums, and strict literal values.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Basic Guide to Zod
  post_tag:
    - array
    - enum
    - literal
    - validation
    - typescript
---

<div class="toc" markdown="1">

## On this Page

- [Validating Arrays](#validating-arrays)
- [Working with Enums](#working-with-enums)
- [Literal Types](#literal-types)
- [Combining Types](#combining-types)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Validating Arrays

To define an array schema, use `z.array(schema)`:

```ts
const TagsSchema = z.array(z.string());

TagsSchema.parse(["typescript", "zod"]); // ✅
TagsSchema.parse(["hello", 42]); // ❌ Error: expected string
```

You can also add constraints like `.min()` or `.max()`:

```ts
const MinTagsSchema = z.array(z.string()).min(1);
```

### Example: List of Users

```ts
const UserSchema = z.object({
  name: z.string(),
});

const UsersSchema = z.array(UserSchema);

UsersSchema.parse([{ name: "Alice" }, { name: "Bob" }]); // ✅
```

## Working with Enums

If a field can only be one of a few values, use `z.enum()`:

```ts
const RoleSchema = z.enum(["admin", "user", "guest"]);

RoleSchema.parse("admin"); // ✅
RoleSchema.parse("manager"); // ❌ not part of enum
```

This automatically infers the TypeScript union type:

```ts
type Role = z.infer<typeof RoleSchema>; 
// ➜ "admin" | "user" | "guest"
```

## Literal Types

If you want to validate a field to match **one specific value**, use `z.literal()`:

```ts
const AcceptTermsSchema = z.literal(true);

AcceptTermsSchema.parse(true); // ✅
AcceptTermsSchema.parse(false); // ❌ must be true
```

This is great for feature toggles, flags, or strict checks.

## Combining Types

You can combine literals and enums:

```ts
const ColorSchema = z.union([
  z.literal("red"),
  z.literal("green"),
  z.literal("blue"),
]);

ColorSchema.parse("green"); // ✅
ColorSchema.parse("yellow"); // ❌
```

Or simply use `z.enum(["red", "green", "blue"])` for the same result, with cleaner syntax.

## Summary

- Use `z.array()` to validate lists of values
- Use `z.enum()` for strict value sets
- Use `z.literal()` for a specific single value
- Combine them for expressive, reusable schemas

---

Next up, we’ll look at **working with nested objects and schema composition** — a must for building real-world APIs and forms.

---

*** Master the Code, Be the Guru! ***

</div>
