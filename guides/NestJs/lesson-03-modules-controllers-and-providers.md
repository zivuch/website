---
title: Modules, Controllers, and Providers
menu_order: 3
post_status: publish
post_excerpt: Learn how to organize your app with NestJS modules, route requests with controllers, and inject logic through providers.
taxonomy:
  category:
    - nestjs
    - Basic Guide to NestJS
  post_tag:
    - typescript
    - nestjs
    - modules
    - controllers
    - providers
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Understanding Modules](#understanding-modules)
- [Creating and Importing a Module](#creating-and-importing-a-module)
- [What is a Controller?](#what-is-a-controller)
- [Defining Routes with Controllers](#defining-routes-with-controllers)
- [What is a Provider?](#what-is-a-provider)
- [Injecting Services into Controllers](#injecting-services-into-controllers)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 01: What is NestJS and Why Use It](./lesson-01-what-is-nestjs-and-why-use-it)
- [Lesson 02: Project Structure and CLI](./lesson-02-project-structure-and-cli)
- [Lesson 03: Modules, Controllers, and Providers](./lesson-03-modules-controllers-and-providers)
- [Lesson 04: Dependency Injection in NestJS](./lesson-04-dependency-injection-in-nestjs)
- [Lesson 05: Routing and HTTP Methods in NestJS](./lesson-05-routing-and-http-methods-in-nestjs)

</div>

</div>

<div class="guru-main" markdown="1">

## Understanding Modules

Every NestJS app is made up of **modules**.

A module is a class annotated with the `@Module()` decorator and is used to group related functionality (controllers, services, and other modules).

```ts
import { Module } from '@nestjs/common';

@Module({
  imports: [],
  controllers: [],
  providers: [],
})
export class UsersModule {}
```

Modules allow your app to remain scalable and loosely coupled.

---

## Creating and Importing a Module

Generate a module using the CLI:

```bash
nest g module users
```

Then import it into the root module:

```ts
import { Module } from '@nestjs/common';
import { UsersModule } from './users/users.module';

@Module({
  imports: [UsersModule],
})
export class AppModule {}
```

---

## What is a Controller?

A **controller** is responsible for handling incoming requests and returning responses.

Use the CLI to generate one:

```bash
nest g controller users
```

Example:

```ts
import { Controller, Get } from '@nestjs/common';

@Controller('users')
export class UsersController {
  @Get()
  findAll() {
    return ['Alice', 'Bob', 'Charlie'];
  }
}
```

Access it via:  
`GET /users`

---

## Defining Routes with Controllers

Controllers use method decorators to handle routes:

- `@Get()`, `@Post()`, `@Put()`, `@Delete()`
- You can pass route paths like `@Get(':id')`

```ts
@Get(':id')
findOne(@Param('id') id: string) {
  return `User ${id}`;
}
```

---

## What is a Provider?

A **provider** is any service, factory, or class that can be injected into other parts of your application via NestJS’s dependency injection system.

Generate one:

```bash
nest g service users
```

Example:

```ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class UsersService {
  findAll() {
    return ['Alice', 'Bob', 'Charlie'];
  }
}
```

---

## Injecting Services into Controllers

You can inject the service into your controller using the constructor:

```ts
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  findAll() {
    return this.usersService.findAll();
  }
}
```

Nest will automatically resolve and inject `UsersService`.

---

## Summary

- **Modules** organize features and logic
- **Controllers** define request handlers
- **Providers** inject reusable logic via services
- This trio is the foundation of every NestJS app

> Next: **Lesson 04 – Dependency Injection in NestJS**

</div>
