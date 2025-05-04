---
title: When to Use Microservices (and When Not To)
menu_order: 6
post_status: publish
post_excerpt: Discover the right time to adopt microservices—and why starting with a monolith might actually save you.
taxonomy:
  category:
    - microservices
  post_tag:
    - architecture decisions
    - monolith vs microservices
    - team size
    - scaling
---

<div class="toc" markdown="1">

<div class="otg" markdown="1">

## On this Page

- [Don’t Start With Microservices](#dont-start-with-microservices)
- [When Microservices Make Sense](#when-microservices-make-sense)
- [Signs You’re Ready](#signs-youre-ready)
- [Red Flags and Anti-Patterns](#red-flags-and-anti-patterns)
- [Migrating from Monolith to Microservices](#migrating-from-monolith-to-microservices)
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

## Don’t Start With Microservices

It’s tempting to build everything “the right way” from the start — but microservices come with complexity:

- DevOps setup
- Networking
- Observability
- Deployment pipelines
- CI/CD and monitoring for multiple services

**If you're an early-stage team or building an MVP, start with a monolith.**  
Split it later when you feel the pain.

---

## When Microservices Make Sense

✅ Use microservices when:

- You have **a growing engineering team** (5+ devs)
- You’re dealing with **clear domain boundaries**
- You need to **scale parts of the system independently**
- You have mature **DevOps, CI/CD, observability**
- You’re hitting bottlenecks in your monolith

---

## Signs You’re Ready

- Your monolith has **modules that change independently**
- You need different **scaling policies** per module
- Your teams are **stepping on each other’s toes** in the codebase
- You want to use **multiple languages or runtimes**
- You're seeing **slow build and deploy times**

---

## Red Flags and Anti-Patterns

❌ Don’t use microservices if:

- You don’t have strong testing/monitoring/devops practices
- You’re a team of 1–3 devs
- You’re not clear on your domain boundaries
- You’re doing it "because Netflix does it"
- You haven’t yet launched your product

> Microservices won’t solve organizational or product problems.

---

## Migrating from Monolith to Microservices

When the time comes, **do it gradually**:

1. Identify bounded contexts (e.g. Auth, Billing, Orders)
2. Extract one service at a time
3. Use API contracts or event publishing to decouple
4. Build monitoring, retries, and fallbacks
5. Let the monolith and microservices coexist during the transition

Example: Extract `AuthService` as the first candidate. It’s usually well-bounded and has few dependencies.

---

## Summary

Microservices aren’t the default — they’re an optimization for scale, speed, and flexibility.  
Start simple, grow complexity **only when the pain justifies it**.

---

You’ve completed the **Basic Guide to Microservices**!

Next up:  
**Advanced Guide to Microservices – Lesson 07: Service Discovery and API Gateways**

</div>
