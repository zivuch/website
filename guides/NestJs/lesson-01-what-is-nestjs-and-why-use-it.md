---
title: What is NestJS and Why Use It?
menu_order: 1
post_status: publish
post_excerpt: An introduction to NestJS — what it is, why it exists, and where it shines in building scalable backend apps.
taxonomy:
  category:
    - nestjs
    - Basic Guide to NestJS
  post_tag:
    - typescript
    - nestjs
    - backend
    - architecture
    - nodejs
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What is NestJS?](#what-is-nestjs)
- [Why Use NestJS Over Express?](#why-use-nestjs-over-express)
- [Core Concepts and Philosophy](#core-concepts-and-philosophy)
- [How NestJS Compares to Other Frameworks](#how-nestjs-compares-to-other-frameworks)
- [What You'll Build with NestJS](#what-youll-build-with-nestjs)
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

## What is NestJS?

NestJS is a **progressive Node.js framework** built with and for **TypeScript**. Inspired by Angular, it brings modular architecture, strong typing, and developer ergonomics to server-side applications.

At its core, Nest uses:

- **Express** (or optionally Fastify) under the hood
- **Decorators and metadata** to define modules, routes, and logic
- **Dependency injection** for clean, testable architecture

> Think of it as Angular for the backend — minus the DOM.

---

## Why Use NestJS Over Express?

Express is great for quick APIs, but it lacks structure for large apps. NestJS solves that with:

| Feature                 | Express | NestJS   |
| ----------------------- | ------- | -------- |
| TypeScript support      | Manual  | Native   |
| Modular architecture    | ❌      | ✅       |
| Dependency injection    | ❌      | ✅       |
| Decorators              | ❌      | ✅       |
| Testing tools           | Basic   | Built-in |
| CLI for scaffolding     | ❌      | ✅       |
| Ready for microservices | ❌      | ✅       |

If your app is growing or will be part of a larger system, NestJS gives you a huge head start.

---

## Core Concepts and Philosophy

NestJS is built on **OOP**, **FP**, and **FRP** principles:

- **Everything is modular**: You structure your app by features, not by type
- **Use decorators** like `@Module()`, `@Controller()`, `@Injectable()` to define architecture
- **Everything is typed**: Routes, services, responses, even middleware

It’s not just a framework — it’s a **design pattern** for clean backends.

---

## How NestJS Compares to Other Frameworks

- ✅ **Express**: More structured and opinionated
- ✅ **Fastify**: Nest can use Fastify internally for better performance
- ✅ **Koa/Hapi**: Nest is more modular and scalable
- ✅ **Spring Boot (Java)**: Nest mimics many of its principles in a TypeScript world

If you're coming from Angular, Java/Spring, or want maintainable Node.js, NestJS feels familiar and powerful.

---

## What You’ll Build with NestJS

With NestJS, you can build:

- RESTful APIs
- GraphQL APIs
- Microservices with Kafka/RMQ
- WebSockets & real-time apps
- CLI tools
- Enterprise-ready services

It’s not just a router — it’s a full platform for scalable architecture.

---

## Summary

NestJS brings architecture, modularity, and strong typing to Node.js development — perfect for TypeScript lovers, growing teams, and clean backend systems.

> Next: **Lesson 02 – NestJS Project Structure and CLI**

</div>
