---
title: Pipes and Custom Decorators
menu_order: 7
post_status: publish
post_excerpt: Learn how to use NestJS pipes to transform and validate input, and how to build reusable custom decorators.
taxonomy:
  category:
    - nestjs
    - Advanced Guide to NestJS
  post_tag:
    - typescript
    - nestjs
    - pipes
    - decorators
    - validation
---

<div class="toc" markdown="1">

<div class="otפ" markdown="1">

## On this Page

- [What is a Pipe?](#what-is-a-pipe)
- [Using Built-in Pipes](#using-built-in-pipes)
- [Creating a Custom Pipe](#creating-a-custom-pipe)
- [What is a Custom Decorator?](#what-is-a-custom-decorator)
- [Creating a Simple Decorator](#creating-a-simple-decorator)
- [Combining Decorators with Metadata](#combining-decorators-with-metadata)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 06: Middleware, Guards, and Interceptors](./lesson-06-middleware-guards-and-interceptors)
- [Lesson 07: Pipes and Custom Decorators in NestJS](./lesson-07-pipes-and-custom-decorators-in-nestjs)
- [Lesson 08: Working with Databases (TypeORM or Prisma)](./lesson-08-working-with-databases-typeorm-or-prisma)
- [Lesson 09: Authentication with Passport and JWT](./lesson-09-authentication-with-passport-and-jwt)
- [Lesson 10: Testing in NestJS](./lesson-10-testing-in-nestjs)

</div>

</div>

<div class="guru-main" markdown="1">

## What is a Pipe?

**Pipes** are classes that implement logic to transform or validate input data before it reaches your route handlers.

You can use pipes to:

- Parse and validate parameters
- Transform request body values
- Throw validation exceptions

---

## Using Built-in Pipes

NestJS includes several useful pipes:

```ts
@Get(':id')
getUser(@Param('id', ParseIntPipe) id: number) {
  return `User ID is ${id}`;
}
```

Common built-in pipes:

- `ParseIntPipe`
- `ParseBoolPipe`
- `ValidationPipe` (used with class-validator)
- `DefaultValuePipe`

---

## Creating a Custom Pipe

Here’s a pipe that trims strings:

```ts
import { PipeTransform, Injectable } from "@nestjs/common";

@Injectable()
export class TrimPipe implements PipeTransform {
  transform(value: any) {
    return typeof value === "string" ? value.trim() : value;
  }
}
```

Usage:

```ts
@Post()
createUser(@Body('name', TrimPipe) name: string) {
  return { name };
}
```

You can also throw exceptions if validation fails:

```ts
if (!value.includes("@")) {
  throw new BadRequestException("Invalid email");
}
```

---

## What is a Custom Decorator?

Custom decorators let you create **reusable metadata or logic wrappers** for route handlers, parameters, or classes.

They’re great for:

- Abstracting repeated logic
- Injecting metadata (like roles)
- Simplifying syntax

---

## Creating a Simple Decorator

Example: `@User()` that extracts the `user` object from the request

```ts
import { createParamDecorator, ExecutionContext } from "@nestjs/common";

export const User = createParamDecorator(
  (data: unknown, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    return request.user;
  }
);
```

Usage:

```ts
@Get('profile')
getProfile(@User() user) {
  return user;
}
```

---

## Combining Decorators with Metadata

Use `@SetMetadata()` and `@Reflector` to define and read custom metadata.

```ts
export const Roles = (...roles: string[]) => SetMetadata("roles", roles);
```

Use this in guards:

```ts
const roles = this.reflector.get<string[]>("roles", context.getHandler());
```

Great for role-based access systems.

---

## Summary

- **Pipes** transform or validate incoming data before it reaches your route
- **Custom decorators** let you simplify, extend, and reuse logic in a clean way
- Together, they give you more control and flexibility in NestJS apps

> Next: **Lesson 08 – Discriminated Unions and Tagged Types**

</div>
