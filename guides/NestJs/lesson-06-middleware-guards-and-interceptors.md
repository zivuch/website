---
title: Middleware, Guards, and Interceptors
menu_order: 6
post_status: publish
post_excerpt: Master NestJS middleware, guards, and interceptors to control requests, access, and execution flow.
taxonomy:
  category:
    - nestjs
    - Advanced Guide to NestJS
  post_tag:
    - typescript
    - nestjs
    - middleware
    - guards
    - interceptors
    - lifecycle
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is Middleware?](#what-is-middleware)
- [Creating and Applying Middleware](#creating-and-applying-middleware)
- [What are Guards?](#what-are-guards)
- [Building an Auth Guard Example](#building-an-auth-guard-example)
- [What are Interceptors?](#what-are-interceptors)
- [Use Case: Logging and Response Transformation](#use-case-logging-and-response-transformation)
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

## What is Middleware?

Middleware functions execute **before** the route handler. They're commonly used for:

- Logging
- Request body manipulation
- Authentication preprocessing
- Rate limiting

```ts
@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: Function) {
    console.log(`[${req.method}] ${req.url}`);
    next();
  }
}
```

Apply it in a module:

```ts
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes("*");
  }
}
```

---

## What are Guards?

**Guards** determine whether a request should proceed. They're used for:

- Role-based access
- Auth token validation
- Conditional routing logic

```ts
@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const req = context.switchToHttp().getRequest();
    return req.headers.authorization === "Bearer valid_token";
  }
}
```

Apply to a route or controller:

```ts
@UseGuards(AuthGuard)
@Get('secure')
getSecureData() {
  return 'Secret data';
}
```

---

## Building an Auth Guard Example

Guards are powerful because they can access route metadata, request objects, and more.

They return:

- `true` to allow the request
- `false` or throw an exception to block

You can combine guards with `@SetMetadata()` and `@Roles()` decorators to build role-based systems.

---

## What are Interceptors?

**Interceptors** wrap around method execution — they can:

- Log before/after
- Transform responses
- Bind additional logic (e.g., timing, caching)

Example:

```ts
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    console.log("Before...");
    const now = Date.now();
    return next
      .handle()
      .pipe(tap(() => console.log(`After... ${Date.now() - now}ms`)));
  }
}
```

Apply globally or at method level:

```ts
@UseInterceptors(LoggingInterceptor)
@Get()
findAll() {
  return ['Alice', 'Bob'];
}
```

---

## Use Case: Logging and Response Transformation

Interceptors can modify the result before sending:

```ts
@Injectable()
export class TransformInterceptor implements NestInterceptor {
  intercept(_, next: CallHandler): Observable<any> {
    return next.handle().pipe(map((data) => ({ status: "success", data })));
  }
}
```

Result:

```json
{
  "status": "success",
  "data": [...]
}
```

---

## Summary

- **Middleware** handles raw requests before they hit controllers
- **Guards** decide whether requests are allowed
- **Interceptors** can transform, wrap, or log response data
- All three play key roles in clean, modular NestJS architecture

> Next: **Lesson 07 – Pipes and Custom Decorators**

</div>
