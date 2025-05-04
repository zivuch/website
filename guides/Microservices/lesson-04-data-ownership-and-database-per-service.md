---
title: Data Ownership and Database Per Service
menu_order: 4
post_status: publish
post_excerpt: Learn why each microservice should own its data and how to avoid shared database pitfalls in distributed systems.
taxonomy:
  category:
    - microservices
  post_tag:
    - database per service
    - data ownership
    - distributed data
    - microservices
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [The Core Principle: Own Your Data](#the-core-principle-own-your-data)
- [What Is the Database Per Service Pattern?](#what-is-the-database-per-service-pattern)
- [Why Sharing Databases Is a Mistake](#why-sharing-databases-is-a-mistake)
- [How Services Exchange Data](#how-services-exchange-data)
- [Data Duplication vs Data Sync](#data-duplication-vs-data-sync)
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

## The Core Principle: Own Your Data

In microservices, **each service is responsible for its own data**.

This means:

- The service owns the database schema
- No other service reads or writes to it directly
- You enforce boundaries between business domains

This leads to **decoupling**, better **autonomy**, and safer **evolution of features**.

---

## What Is the Database Per Service Pattern?

It simply means:

> Every microservice has its **own private database**.

✅ Allowed:

- AuthService → auth_db
- OrderService → orders_db
- NotificationService → notifications_db

❌ Not Allowed:

- Shared customer table accessed by 4 services
- One big "global" DB for all services

Each DB can use a different:

- Technology (PostgreSQL, MongoDB, etc.)
- Schema design
- Scaling model

---

## Why Sharing Databases Is a Mistake

Sharing a database tightly couples services.

Problems include:

- Hard to change schema (ripple effects)
- Impossible to isolate failures
- Difficult to scale independently
- Codebases must coordinate changes

Think of shared DBs as **a hidden monolith**.

---

## How Services Exchange Data

Instead of querying another service’s database, do this:

**Option 1: Call an API**

```ts
GET /users/:id
```

**Option 2: Subscribe to an event**

```ts
event: UserCreated;
payload: {
  id, email, createdAt;
}
```

The owning service exposes controlled, versioned interfaces.  
Other services treat it like a black box.

---

## Data Duplication vs Data Sync

Yes — duplication is allowed and expected in microservices.

> "Duplication is better than the wrong kind of coupling."

Example:

- OrderService **stores** a copy of the user’s name/email at the time of order
- Even if the UserService changes later, past orders remain intact

Don’t sync everything in real-time unless you absolutely need to.  
Use eventual consistency and publish events for updates.

---

## Summary

Microservices should not share databases.  
Each service must fully own its data and expose it via APIs or events.  
This keeps services independent, reliable, and scalable.

---

Next:  
**Lesson 05 – Service Deployment, Scaling, and Failure Isolation**

</div>
