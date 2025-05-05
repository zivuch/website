---
title: Dependency Injection in NestJS
menu_order: 4
post_status: publish
post_excerpt: Understand how dependency injection works in NestJS and how it powers services, testing, and scalability.
taxonomy:
  category:
    - nestjs
    - Basic Guide to NestJS
  post_tag:
    - typescript
    - nestjs
    - dependency injection
    - services
    - providers
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is Dependency Injection?](#what-is-dependency-injection)
- [How NestJS Uses DI](#how-nestjs-uses-di)
- [Injecting Services into Controllers](#injecting-services-into-controllers)
- [Injecting Custom Providers](#injecting-custom-providers)
- [DI Scope: Default, Request, and Transient](#di-scope-default-request-and-transient)
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

## What is Dependency Injection?

**Dependency Injection (DI)** is a design pattern where components (like services) are provided to a class rather than created by it.

In NestJS:
- You don’t `new` your services manually
- You declare dependencies in the constructor
- Nest resolves and provides those automatically

---

## How NestJS Uses DI

Nest uses **TypeScript reflection** and decorators like `@Injectable()` to manage dependencies.

```ts
@Injectable()
export class UsersService {
  getUsers() {
    return ['Alice', 'Bob'];
  }
}
```

Then inject the service like so:

```ts
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  getAll() {
    return this.usersService.getUsers();
  }
}
```

---

## Injecting Services into Controllers

This is the most common usage of DI:

- Mark your service with `@Injectable()`
- Add it to your module’s `providers`
- Inject it into your controller via the constructor

No need to import or instantiate manually — Nest handles that for you.

---

## Injecting Custom Providers

You can also create and inject **custom tokens**, such as config values or factories:

```ts
const CONFIG_TOKEN = 'CONFIG_TOKEN';

@Module({
  providers: [
    {
      provide: CONFIG_TOKEN,
      useValue: { appName: 'MyApp' },
    },
  ],
})
export class AppModule {}
```

Inject it anywhere:

```ts
@Injectable()
export class SomeService {
  constructor(@Inject(CONFIG_TOKEN) private config: any) {}
}
```

---

## DI Scope: Default, Request, and Transient

Nest supports **three DI scopes**:

| Scope     | Description |
|-----------|-------------|
| `default` | Singleton – one instance for the app lifecycle |
| `request` | New instance per request (useful with `@Req`) |
| `transient` | New instance per injection point (very isolated) |

To use a scope:

```ts
@Injectable({ scope: Scope.REQUEST })
export class MyScopedService {}
```

Import `Scope` from `@nestjs/common`.

---

## Summary

Dependency injection is the secret sauce of NestJS — it allows you to write loosely coupled, testable, and maintainable code by offloading the responsibility of managing class dependencies to the framework itself.

> Next: **Lesson 05 – Routing and HTTP Methods in NestJS**

</div>
