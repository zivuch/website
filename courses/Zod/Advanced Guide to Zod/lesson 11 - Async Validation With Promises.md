---
title: Async Validation with Promises in Zod
menu_order: 11
post_status: publish
taxonomy:
  category:
    - zod
  post_tag:
    - async
    - validation
    - promise
    - refineAsync
    - advanced zod
---

<div class="toc" markdown="1">

## On this Page

- [Why Async Validation?](#why-async-validation)
- [Using refineAsync()](#using-refineasync)
- [Validating Async Data Sources](#validating-async-data-sources)
- [Using z.promise()](#using-zpromise)
- [Caveats and Best Practices](#caveats-and-best-practices)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Async Validation?

Some validation rules can’t be checked synchronously:

- Is this email already taken?
- Does the user exist in the database?
- Did a remote API respond successfully?

Zod supports **asynchronous validation** with methods like `.refineAsync()` and schema types like `z.promise()`.

---

## Using `refineAsync()`

It works just like `.refine()`, but returns a promise:

```ts
const EmailSchema = z
  .string()
  .email()
  .refineAsync(async (email) => {
    const isTaken = await fakeCheckEmail(email);
    return !isTaken;
  }, {
    message: "Email already in use",
  });

async function fakeCheckEmail(email: string) {
  return email === "taken@example.com"; // Simulated DB check
}
```

### Usage

You must use `await` with `.parseAsync()`:

```ts
const result = await EmailSchema.parseAsync("taken@example.com");
// ❌ Throws: Email already in use
```

---

## Validating Async Data Sources

You can validate an entire schema asynchronously:

```ts
const RegisterSchema = z.object({
  username: z.string(),
  email: z.string().email(),
}).refineAsync(async (data) => {
  return !(await isUserTaken(data.username));
}, {
  message: "Username already taken",
  path: ["username"],
});
```

This lets you apply async logic **with context and specific field paths**.

---

## Using `z.promise()`

Sometimes your schema *returns* a promise. You can validate that too:

```ts
const AsyncNumberSchema = z.promise(z.number());

AsyncNumberSchema.parse(Promise.resolve(42)); // ✅
AsyncNumberSchema.parse(Promise.resolve("hello")); // ❌
```

Zod will wait for the promise to resolve and validate the result.

---

## Caveats and Best Practices

- Always use `.parseAsync()` or `.safeParseAsync()` when your schema uses `refineAsync()`
- Avoid mixing sync and async `parse()` — it's easy to forget
- Use `.superRefine()` and `ctx.addIssue()` if you need detailed async logic across multiple fields

---

## Summary

- Use `.refineAsync()` for async field-level validation
- Use `.parseAsync()` or `.safeParseAsync()` to validate data that involves `await`
- Use `z.promise()` to validate promise-returning values
- Async validation is ideal for working with remote APIs and databases

---

Next: **Lesson 12 – Building Reusable Schemas Across Frontend and Backend**

---

*** Master the Code, Be the Guru! ***

</div>
