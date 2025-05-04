---
title: Key Concepts – Bounded Contexts, Services, and APIs
menu_order: 2
post_status: publish
post_excerpt: Learn the foundational concepts that define how microservices are scoped, separated, and communicate.
taxonomy:
  category:
    - microservices
  post_tag:
    - bounded context
    - service boundaries
    - rest api
    - domain-driven design
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What Is a Bounded Context?](#what-is-a-bounded-context)
- [Defining a Service](#defining-a-service)
- [Service Contracts and APIs](#service-contracts-and-apis)
- [Avoiding Tight Coupling](#avoiding-tight-coupling)
- [Common Mistakes](#common-mistakes)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 01: Introduction to Microservices Architecture](./lesson-01-introduction-to-microservices-architecture)
- [Lesson 02: Key Concepts – Bounded Contexts, Services, and APIs](./lesson-02-key-concepts-bounded-contexts-services-and-apis)
- [Lesson 03: Service Communication Patterns – Sync, Async, Events, and Queues](./lesson-03-service-communication-patterns-sync-async-events-and-queues)
- [Lesson 04: Data Ownership and Database Per Service](./lesson-04-data-ownership-and-database-per-service)
- [Lesson 05: Service Deployment, Scaling, and Failure Isolation](./lesson-05-service-deployment-scaling-and-failure-isolation)
- [Lesson 06: When to Use Microservices (and When Not To)](./lesson-06-when-to-use-microservices-and-when-not-to)

</div>
</div>

<div class="guru-main" markdown="1">

## What Is a Bounded Context?

In microservices, a **bounded context** defines the boundary of a business capability or domain area.

This concept comes from **Domain-Driven Design (DDD)**:

- Each service lives in its own "context" (e.g., `User`, `Payments`, `Orders`)
- Each context owns its **language**, **logic**, and **data**

Think of it as:

> “A clearly defined scope in which a specific domain model applies.”

Example:

- `AuthService` handles user registration and login
- `BillingService` handles subscriptions and invoices

Each has its own **purpose**, **team**, and **responsibility**.

---

## Defining a Service

A **microservice** should:

- Represent a complete feature or business function
- Own its data and lifecycle
- Be deployable independently

Good service boundaries:

- Auth
- Payments
- Inventory
- Notifications

Bad boundaries:

- UserFirstNameService
- ButtonClickService
- "EverythingInOneService"

---

## Service Contracts and APIs

Services communicate via well-defined **contracts**, usually over:

- **HTTP (REST)** – widely used, language-agnostic
- **gRPC** – fast, binary-based communication
- **Message queues (Kafka, RabbitMQ)** – for async, event-based flows

Each service exposes a **stable, versioned API** — clients depend on the contract, not the internal logic.

Keep APIs backward-compatible as long as possible.

---

## Avoiding Tight Coupling

Coupling = one service depending directly on another’s logic or database.

❌ Bad:

- `InventoryService` queries `OrdersService` DB directly

✅ Good:

- `OrdersService` **calls** `InventoryService` API or sends an **event**

Tips:

- Never share databases between services
- Favor async messaging where possible
- Keep schemas internal unless explicitly shared

---

## Common Mistakes

- ❌ Designing services by database tables instead of business capabilities
- ❌ Splitting services too early without clear ownership
- ❌ Treating microservices as mini-monoliths with tight internal coupling
- ❌ Sharing internal models or logic between services

---

## Summary

Bounded contexts help you define clean service boundaries. Microservices communicate through versioned APIs, not shared databases. This separation keeps systems modular, scalable, and easier to evolve over time.

---

Next up:  
**Lesson 03 – Service Communication Patterns: Sync, Async, Events, and Queues**

</div>
