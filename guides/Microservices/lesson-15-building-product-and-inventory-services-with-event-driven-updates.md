---
title: Building Product and Inventory Services (with Event-Driven Updates)
menu_order: 15
post_status: publish
post_excerpt: Create loosely coupled Product and Inventory services and link them using async events for stock updates.
taxonomy:
  category:
    - microservices
  post_tag:
    - product service
    - inventory service
    - event driven
    - messaging
    - kafka
    - rabbitmq
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Service Responsibilities](#service-responsibilities)
- [Tech Stack and Messaging Layer](#tech-stack-and-messaging-layer)
- [ProductService Overview](#productservice-overview)
- [InventoryService Overview](#inventoryservice-overview)
- [Publishing and Listening to Events](#publishing-and-listening-to-events)
- [Event Format and Schema](#event-format-and-schema)
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

## Service Responsibilities

### ProductService
- Manage product catalog (title, description, price)
- Expose endpoints to list, create, update products
- **Emit events** when a product is added or updated

### InventoryService
- Maintain real-time stock levels for each product
- Listen for product creation/update events
- Allow updates via internal admin API or order events

---

## Tech Stack and Messaging Layer

Both services use:
- **Node.js + TypeScript**
- **Express**
- **MongoDB**
- **Kafka** (or RabbitMQ) for event transport

Use a shared messaging utility with a wrapper:
```ts
publishEvent('product.created', { productId, title, price });
```

---

## ProductService Overview

### Product Model
```ts
const ProductSchema = new mongoose.Schema({
  title: String,
  description: String,
  price: Number,
});
```

### Create Product + Emit Event
```ts
router.post('/products', async (req, res) => {
  const product = await Product.create(req.body);
  publishEvent('product.created', {
    productId: product._id,
    title: product.title,
    price: product.price
  });
  res.status(201).json(product);
});
```

---

## InventoryService Overview

### Inventory Model
```ts
const InventorySchema = new mongoose.Schema({
  productId: String,
  quantity: Number,
});
```

### Event Listener
```ts
subscribeToEvent('product.created', async (data) => {
  await Inventory.create({ productId: data.productId, quantity: 0 });
});
```

Now inventory is aware of all new products — no direct HTTP needed!

---

## Publishing and Listening to Events

Use a lightweight event bus or a wrapper over Kafka or RabbitMQ.

### Example Event Bus Wrapper
```ts
// bus.ts
export const publishEvent = (type: string, payload: any) => {
  kafkaProducer.send({ topic: type, messages: [{ value: JSON.stringify(payload) }] });
};

export const subscribeToEvent = (type: string, handler: Function) => {
  kafkaConsumer.subscribe({ topic: type });
  kafkaConsumer.run({
    eachMessage: async ({ message }) => {
      const payload = JSON.parse(message.value.toString());
      handler(payload);
    },
  });
};
```

---

## Event Format and Schema

Define a consistent schema for your events:
```json
{
  "type": "product.created",
  "data": {
    "productId": "abc123",
    "title": "iPhone 15",
    "price": 999
  },
  "timestamp": "2025-04-30T12:00:00Z"
}
```

Use `zod` to validate event payloads on both publish and consume.

---

## Summary

By decoupling `ProductService` and `InventoryService` using events, we enable flexible scaling and loose coupling. Each service handles its own data and logic, and they stay in sync asynchronously.

---

Next up:  
**Lesson 16 – Order and Payment Services: Choreography vs Orchestration**

</div>
