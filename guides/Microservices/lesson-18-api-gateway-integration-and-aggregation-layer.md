---
title: API Gateway Integration and Aggregation Layer
menu_order: 18
post_status: publish
post_excerpt: Unify access to your microservices using an API Gateway and learn how to aggregate data from multiple services.
taxonomy:
  category:
    - microservices
  post_tag:
    - api gateway
    - service aggregation
    - graphql
    - reverse proxy
    - backend for frontend
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What Is an API Gateway?](#what-is-an-api-gateway)
- [Why Use a Gateway in Microservices?](#why-use-a-gateway-in-microservices)
- [Gateway Responsibilities](#gateway-responsibilities)
- [Implementing a Basic Gateway (Express + Proxy)](#implementing-a-basic-gateway-express--proxy)
- [Aggregation Layer (BFF or GraphQL)](#aggregation-layer-bff-or-graphql)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 13: Designing a Real-World Microservice System](./lesson-13-designing-a-real-world-microservice-system)
- [Lesson 14: Building a Service – User Registration and Authentication](./lesson-14-building-a-service-user-registration-and-authentication)
- [Lesson 15: Building Product and Inventory Services (with Event-Driven Updates)](./lesson-15-building-product-and-inventory-services-with-event-driven-updates)
- [Lesson 16: Order and Payment Services – Choreography vs Orchestration](./lesson-16-order-and-payment-services-choreography-vs-orchestration)
- [Lesson 17: Building an Event Bus and Shared Messaging Utility](./lesson-17-building-an-event-bus-and-shared-messaging-utility)
- [Lesson 18: API Gateway Integration and Aggregation Layer](./lesson-18-api-gateway-integration-and-aggregation-layer)
- [Lesson 19: Testing and Debugging Microservices](./lesson-19-testing-and-debugging-microservices)
- [Lesson 20: Final Thoughts, Best Practices, and Resources](./lesson-20-final-thoughts-best-practices-and-resources)

</div>

</div>


<div class="guru-main" markdown="1">

## What Is an API Gateway?

An **API Gateway** is the entry point for all client requests in a microservices system.

It routes, aggregates, transforms, and protects traffic between clients and services.

You can think of it as the **traffic controller** for your backend.

---

## Why Use a Gateway in Microservices?

Without a gateway:
- Clients must know internal service URLs
- Every client must handle service changes
- Cross-cutting concerns (auth, rate limit, logging) are repeated

With a gateway:
✅ Simplified client access  
✅ Centralized security and monitoring  
✅ Flexible routing and aggregation  

---

## Gateway Responsibilities

An API Gateway can handle:

- Reverse proxying
- Request routing
- Rate limiting
- Authentication (e.g., JWT validation)
- Aggregation (multiple services → one response)
- Caching
- Load balancing
- Logging and metrics

Tools:
- **Kong**
- **NGINX**
- **Traefik**
- **Express (custom gateway)**
- **BFF or GraphQL Gateway**

---

## Implementing a Basic Gateway (Express + Proxy)

```ts
// gateway.ts
import express from 'express';
import proxy from 'express-http-proxy';

const app = express();

app.use('/users', proxy('http://user-service:3001'));
app.use('/products', proxy('http://product-service:3002'));
app.use('/orders', proxy('http://order-service:3003'));

app.listen(3000, () => console.log('API Gateway running on port 3000'));
```

Add auth middleware if needed:
```ts
app.use('/orders', verifyJWT, proxy('http://order-service:3003'));
```

---

## Aggregation Layer (BFF or GraphQL)

Sometimes the frontend needs data from multiple services.

Instead of making 3 HTTP calls from the client:
```ts
GET /users/me  
GET /orders?userId=123  
GET /notifications?userId=123
```

Build an **aggregation layer**:
- **BFF** (Backend for Frontend)
- **GraphQL Gateway** (Apollo, Hasura, StepZen)

Example: GraphQL query to combine user + orders
```graphql
{
  me {
    name
    email
    orders {
      id
      total
    }
  }
}
```

The gateway resolves data from multiple services and returns it as one JSON response.

---

## Summary

An **API Gateway** simplifies communication between clients and services by routing, protecting, and aggregating requests. You can implement it as a reverse proxy or a full GraphQL-powered data orchestrator.

---

Next:  
**Lesson 19 – Testing and Debugging Microservices**

</div>
