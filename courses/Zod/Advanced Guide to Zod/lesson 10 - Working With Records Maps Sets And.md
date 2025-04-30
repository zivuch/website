---
title: Working with Records, Maps, Sets, and Enums in Zod
menu_order: 10
post_status: publish
taxonomy:
  category:
    - zod
  post_tag:
    - record
    - map
    - set
    - enum
    - advanced zod
---

<div class="toc" markdown="1">

## On this Page

- [Using z.record()](#using-zrecord)
- [Working with z.map()](#working-with-zmap)
- [Validating Sets with z.set()](#validating-sets-with-zset)
- [Creating Enums with z.enum()](#creating-enums-with-zenum)
- [Using Native TypeScript Enums](#using-native-typescript-enums)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Using `z.record()`

`z.record()` defines objects with dynamic keys (like dictionaries or hash maps).

### Example: Key-value object of strings

```ts
const StringMap = z.record(z.string());

StringMap.parse({
  en: "Hello",
  fr: "Bonjour",
  he: "שלום",
}); // ✅
```

All values must match the provided schema.

### Example: Nested object values

```ts
const ScoreMap = z.record(
  z.object({ score: z.number(), passed: z.boolean() })
);

ScoreMap.parse({
  math: { score: 95, passed: true },
  history: { score: 82, passed: true },
}); // ✅
```

---

## Working with `z.map()`

Zod supports the native JavaScript `Map` object:

```ts
const mapSchema = z.map(z.string(), z.number());

mapSchema.parse(
  new Map([
    ["a", 1],
    ["b", 2],
  ])
); // ✅
```

Useful when using `Map` instances instead of plain objects.

---

## Validating Sets with `z.set()`

Zod can validate JavaScript `Set` objects too:

```ts
const setSchema = z.set(z.string());

setSchema.parse(new Set(["apple", "banana"])); // ✅
```

You can also enforce minimum or maximum size:

```ts
const limitedSet = z.set(z.number()).min(2).max(5);
```

---

## Creating Enums with `z.enum()`

Zod's `z.enum()` creates a strict list of allowed string values:

```ts
const RoleSchema = z.enum(["admin", "user", "guest"]);

RoleSchema.parse("admin"); // ✅
RoleSchema.parse("manager"); // ❌
```

Zod will infer a union type automatically:

```ts
type Role = z.infer<typeof RoleSchema>;
// ➜ "admin" | "user" | "guest"
```

### Getting Enum Options

```ts
RoleSchema.options; // ➜ ["admin", "user", "guest"]
```

---

## Using Native TypeScript Enums

Zod also supports TypeScript enums:

```ts
enum Direction {
  Up = "up",
  Down = "down",
}

const DirectionSchema = z.nativeEnum(Direction);

DirectionSchema.parse("up"); // ✅
DirectionSchema.parse(Direction.Down); // ✅
```

Great for working with shared enums across front-end and back-end apps.

---

## Summary

- Use `z.record()` for key-value objects with unknown keys
- Use `z.map()` and `z.set()` for native JS `Map` and `Set` support
- Use `z.enum()` for strict union types and validation
- Use `z.nativeEnum()` when working with TypeScript enums

---

Next: **Lesson 11 – Zod and Async Validation with Promises**

---

*** Master the Code, Be the Guru! ***

</div>
