---
title: Routing and HTTP Methods in NestJS
menu_order: 5
post_status: publish
post_excerpt: Learn how to define routes, use HTTP method decorators, and handle dynamic parameters in NestJS controllers.
taxonomy:
  category:
    - nestjs
    - Basic Guide to NestJS
  post_tag:
    - typescript
    - nestjs
    - routing
    - http
    - controllers
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Defining Routes with Controllers](#defining-routes-with-controllers)
- [Using HTTP Method Decorators](#using-http-method-decorators)
- [Handling Route Parameters](#handling-route-parameters)
- [Using Query Parameters](#using-query-parameters)
- [Sending JSON and Status Codes](#sending-json-and-status-codes)
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

## Defining Routes with Controllers

In NestJS, routes are defined in **controllers** using the `@Controller()` decorator and method-level decorators for HTTP verbs.

```ts
@Controller('users')
export class UsersController {
  @Get()
  findAll() {
    return ['Alice', 'Bob'];
  }
}
```

This route responds to:  
`GET /users`

---

## Using HTTP Method Decorators

You can use the following decorators to define your route handlers:

- `@Get()` – handle GET requests
- `@Post()` – handle POST requests
- `@Put()` – handle PUT requests
- `@Delete()` – handle DELETE requests
- `@Patch()` – handle PATCH requests
- `@All()` – handle all HTTP methods

```ts
@Post()
create(@Body() data: CreateUserDto) {
  return { message: 'User created', data };
}
```

---

## Handling Route Parameters

Use `@Param()` to extract dynamic segments from the route path:

```ts
@Get(':id')
findOne(@Param('id') id: string) {
  return `User ID: ${id}`;
}
```

Matches: `GET /users/123`

---

## Using Query Parameters

Use `@Query()` to extract URL query parameters:

```ts
@Get()
findFiltered(@Query('role') role: string) {
  return `Filtering by role: ${role}`;
}
```

Matches: `GET /users?role=admin`

You can also extract the entire query object:

```ts
find(@Query() query: any) {
  return query;
}
```

---

## Sending JSON and Status Codes

NestJS will automatically serialize returned objects to JSON.  
To send custom responses or status codes, use `@Res()` or decorators like `@HttpCode()`:

```ts
@HttpCode(204)
@Delete(':id')
remove(@Param('id') id: string) {
  return;
}
```

---

## Summary

- Use decorators to create clear and expressive route handlers
- NestJS maps controller methods to HTTP routes using metadata
- Easily extract params, queries, and bodies with built-in decorators

> Next: Start the **Advanced Guide to NestJS**  
→ **Lesson 06 – Middleware, Guards, and Interceptors**

</div>
