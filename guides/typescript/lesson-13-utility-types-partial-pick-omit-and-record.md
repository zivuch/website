---
title: Utility Types – Partial, Pick, Omit, Record, and More
menu_order: 13
post_status: publish
post_excerpt: Go beyond Partial and Pick – explore TypeScript's full set of utility types and learn to create your own custom helpers.
taxonomy:
  category:
    - typescript
    - Advanced Guide to TypeScript
  post_tag:
    - typescript
    - utility types
    - partial
    - pick
    - omit
    - returntype
    - deeppartial
    - mutable
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Built-in Utility Types](#built-in-utility-types)
  - [`Partial<T>`](#partialt)
  - [`Required<T>`](#requiredt)
  - [`Readonly<T>`](#readonlyt)
  - [`Pick<T, K>`](#pickt-k)
  - [`Omit<T, K>`](#omitt-k)
  - [`Record<K, T>`](#recordk-t)
  - [`ReturnType<T>`](#returntypet)
  - [`Parameters<T>`](#parameterst)
  - [`NonNullable<T>`](#nonnullablet)
  - [`Awaited<T>`](#awaitedt)
- [Custom Utility Types](#custom-utility-types)
  - [`DeepPartial<T>`](#deeppartialt)
  - [`Mutable<T>`](#mutablet)
  - [`DeepReadonly<T>`](#deepreadonlyt)
- [Summary Table](#summary-table)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 11: Generics in Functions and Interfaces](./lesson-11-generics-in-functions-and-interfaces)
- [Lesson 12: Generic Constraints and Default Types](./lesson-12-generic-constraints-and-default-types)
- [Lesson 13: Utility Types: Partial, Pick, Omit, and Record](./lesson-13-utility-types-partial-pick-omit-and-record)
- [Lesson 14: Mapped Types and Keyof](./lesson-14-mapped-types-and-keyof)
- [Lesson 15: Conditional Types and Infer Keyword](./lesson-15-conditional-types-and-infer-keyword)

</div>

</div>

<div class="guru-main" markdown="1">

## Built-in Utility Types

TypeScript provides several built-in utility types that let you transform, manipulate, and reuse existing types in a powerful way.

---

### `Partial<T>`

Makes all properties in a type optional:

```ts
interface User {
  id: number;
  name: string;
}

type UpdateUser = Partial<User>;
// { id?: number; name?: string }
```

---

### `Required<T>`

Makes all optional properties required:

```ts
type User = {
  id?: number;
  name?: string;
};

type FullUser = Required<User>; // { id: number; name: string }
```

---

### `Readonly<T>`

Locks all properties as read-only:

```ts
type Config = {
  port: number;
};

const settings: Readonly<Config> = {
  port: 3000
};

settings.port = 4000; // ❌ Error
```

---

### `Pick<T, K>`

Creates a type by selecting a subset of keys:

```ts
type UserPreview = Pick<User, "id" | "name">;
```

---

### `Omit<T, K>`

Creates a type excluding specific keys:

```ts
type UserForm = Omit<User, "id">;
```

---

### `Record<K, T>`

Constructs an object type with specific keys:

```ts
type Roles = "admin" | "user";

const permissions: Record<Roles, boolean> = {
  admin: true,
  user: false,
};
```

---

### `ReturnType<T>`

Extracts the return type of a function:

```ts
function getUser() {
  return { id: 1, name: "Ziv" };
}

type User = ReturnType<typeof getUser>;
```

---

### `Parameters<T>`

Gets the parameter types of a function:

```ts
function greet(name: string, age: number): void {}

type GreetArgs = Parameters<typeof greet>; // [string, number]
```

---

### `NonNullable<T>`

Removes `null` and `undefined`:

```ts
type Name = string | null | undefined;

type SafeName = NonNullable<Name>; // string
```

---

### `Awaited<T>`

Unwraps the resolved type of a Promise:

```ts
type Data = Promise<{ id: number }>;

type Resolved = Awaited<Data>; // { id: number }
```

---

## Custom Utility Types

These utilities can be created manually using mapped types and conditional logic.

---

### `DeepPartial<T>`

Recursively makes all fields optional:

```ts
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};
```

Usage:

```ts
type Post = {
  id: number;
  meta: {
    title: string;
    tags: string[];
  };
};

type PostDraft = DeepPartial<Post>;
```

---

### `Mutable<T>`

Removes `readonly` from all properties:

```ts
type Mutable<T> = {
  -readonly [P in keyof T]: T[P];
};
```

```ts
type Locked = {
  readonly id: number;
};

type Editable = Mutable<Locked>; // { id: number }
```

---

### `DeepReadonly<T>`

Makes all properties deeply readonly:

```ts
type DeepReadonly<T> = {
  readonly [P in keyof T]: T[P] extends object ? DeepReadonly<T[P]> : T[P];
};

type AppState = {
  user: {
    id: number;
    name: string;
  };
};

type LockedState = DeepReadonly<AppState>;
```

---

## Summary Table

| Utility Type       | Description                                       |
|--------------------|---------------------------------------------------|
| `Partial<T>`       | Makes properties optional                         |
| `Required<T>`      | Makes properties required                         |
| `Readonly<T>`      | Makes properties read-only                        |
| `Pick<T, K>`       | Selects specific properties                       |
| `Omit<T, K>`       | Removes specific properties                       |
| `Record<K, T>`     | Constructs object type with fixed keys            |
| `ReturnType<T>`    | Extracts return type of a function                |
| `Parameters<T>`    | Extracts parameters of a function                 |
| `NonNullable<T>`   | Removes `null` and `undefined`                   |
| `Awaited<T>`       | Unwraps the type a Promise resolves to           |
| `DeepPartial<T>`   | Custom – Makes nested fields optional             |
| `Mutable<T>`       | Custom – Removes `readonly` modifiers             |
| `DeepReadonly<T>`  | Custom – Makes all nested fields readonly         |

Up next: **Lesson 14 – Mapped Types and `keyof`** — transform object types dynamically.

</div>
