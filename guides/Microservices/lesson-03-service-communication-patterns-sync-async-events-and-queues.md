---
title: Service Communication Patterns – Sync, Async, Events, and Queues
menu_order: 3
post_status: publish
post_excerpt: Understand how microservices talk to each other using REST, gRPC, events, and queues—and when to choose each.
taxonomy:
  category:
    - microservices
  post_tag:
    - service communication
    - messaging
    - rest
    - grpc
    - event-driven
---

<div class="toc" markdown="1">

## On this Page

- [Synchronous vs Asynchronous Communication](#synchronous-vs-asynchronous-communication)
- [REST and gRPC](#rest-and-grpc)
- [Event-Driven Architecture](#event-driven-architecture)
- [Using Message Queues](#using-message-queues)
- [When to Choose Which](#when-to-choose-which)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Synchronous vs Asynchronous Communication

There are two primary ways microservices can talk to each other:

**Synchronous (Sync)**  
- One service directly requests data from another
- Immediate response is expected
- Examples: `REST`, `gRPC`

**Asynchronous (Async)**  
- Services emit messages or events
- Receivers process them at their own pace
- Examples: `Kafka`, `RabbitMQ`, `AWS SNS/SQS`

🧠 Think:
- Sync = **Phone call**
- Async = **Email**

---

## REST and gRPC

### REST (HTTP/JSON)
- Simple, readable
- Widely supported
- Slower due to JSON parsing and headers
- Great for public APIs

### gRPC (HTTP/2 + Protocol Buffers)
- Faster and smaller
- Strong typing via `.proto` files
- Requires code generation and tooling
- Ideal for internal microservice calls

📌 REST is often used for **external** APIs  
📌 gRPC is ideal for **internal** service-to-service calls at scale

---

## Event-Driven Architecture

In event-driven systems:
- A service **emits an event** (e.g. `UserCreated`)
- Other services **react** to that event if relevant

Benefits:
- Loose coupling
- Easy to add listeners without changing emitters
- Good for **audit logs**, **notifications**, **automation**, etc.

Example:
```
UserService -> emits UserCreated event
EmailService -> listens and sends welcome email
AnalyticsService -> listens and logs user metrics
```

---

## Using Message Queues

Message brokers help deliver messages reliably and decouple senders from receivers.

Popular choices:
- **RabbitMQ** – push-based, queues
- **Kafka** – high throughput, distributed log
- **NATS** – lightweight and fast

Common patterns:
- **Publish/Subscribe** – fire-and-forget events
- **Work Queue** – background jobs (e.g. thumbnail generation)

Use cases:
- Billing
- Retry handling
- Data sync
- Email jobs

---

## When to Choose Which

| Pattern       | Use When...                                |
|---------------|---------------------------------------------|
| REST          | Simplicity, public APIs, CRUD services      |
| gRPC          | Internal service-to-service, performance-critical |
| Events        | Decoupled workflows, side effects           |
| Queues        | Background tasks, retries, traffic spikes   |

🧩 Mix patterns! Use REST for user-facing APIs and async for internal processing.

---

## Summary

Microservices use both **synchronous** (REST, gRPC) and **asynchronous** (events, queues) communication. Choose the right tool based on latency, reliability, and coupling requirements.

---

Next:  
**Lesson 04 – Data Ownership and Database Per Service**

</div>
