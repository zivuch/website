---
title: Building an Event Bus and Shared Messaging Utility
menu_order: 17
post_status: publish
post_excerpt: Create a shared event bus layer to publish and subscribe to events across your microservices using Kafka or RabbitMQ.
taxonomy:
  category:
    - microservices
  post_tag:
    - event bus
    - messaging
    - kafka
    - rabbitmq
    - nodejs
    - shared utils
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why You Need an Event Bus Abstraction](#why-you-need-an-event-bus-abstraction)
- [Standardizing Event Structure](#standardizing-event-structure)
- [Creating a Messaging Wrapper](#creating-a-messaging-wrapper)
- [Kafka/RabbitMQ Integration Example](#kafkarabbitmq-integration-example)
- [Usage in Microservices](#usage-in-microservices)
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

## Why You Need an Event Bus Abstraction

In distributed systems, services need to **emit and consume events**.  
Doing this directly with Kafka, RabbitMQ, or NATS in every service is:

- ❌ Repetitive
- ❌ Inconsistent
- ❌ Error-prone

✅ Instead, build a shared utility (`event-bus`) to:
- Publish events
- Subscribe to events
- Enforce schemas
- Handle reconnections

---

## Standardizing Event Structure

Design a consistent payload format:

```ts
type BaseEvent<T> = {
  type: string;
  data: T;
  timestamp: string;
};
```

Example event:
```json
{
  "type": "order.created",
  "data": {
    "orderId": "abc123",
    "items": [ ... ]
  },
  "timestamp": "2025-04-30T12:00:00Z"
}
```

Use `zod` to validate event payloads before sending or processing.

---

## Creating a Messaging Wrapper

### `event-bus.ts`

```ts
import { Kafka } from 'kafkajs';

const kafka = new Kafka({ clientId: 'core', brokers: ['localhost:9092'] });
const producer = kafka.producer();
const consumer = kafka.consumer({ groupId: 'service-group' });

export const publishEvent = async (type: string, data: any) => {
  const event = {
    type,
    data,
    timestamp: new Date().toISOString()
  };
  await producer.send({
    topic: type,
    messages: [{ value: JSON.stringify(event) }]
  });
};

export const subscribeToEvent = async (
  type: string,
  handler: (data: any) => void
) => {
  await consumer.subscribe({ topic: type });
  await consumer.run({
    eachMessage: async ({ message }) => {
      const payload = JSON.parse(message.value!.toString());
      handler(payload.data);
    }
  });
};
```

✅ Now every service just imports and uses `publishEvent()` and `subscribeToEvent()`.

---

## Kafka/RabbitMQ Integration Example

For RabbitMQ, you can wrap:
- `amqplib` for basic queues
- `rascal` for advanced use cases

For Kafka:
- Use `kafkajs` (JS)
- Use `confluent-kafka` (high-performance)

If you're using NATS:
- Wrap `nats.connect()` with `.publish()` and `.subscribe()` helpers

Tip: Keep connection logic shared and testable. Don't duplicate it per service.

---

## Usage in Microservices

### ProductService
```ts
await publishEvent('product.created', { productId, title, price });
```

### InventoryService
```ts
await subscribeToEvent('product.created', async (data) => {
  await createInventoryRecord(data.productId);
});
```

Simple, testable, and consistent across services.

---

## Summary

A centralized **Event Bus utility** allows you to decouple event logic from business logic. It makes your microservices easier to test, extend, and reason about — regardless of the messaging platform behind it.

---

Next up:  
**Lesson 18 – API Gateway Integration and Aggregation Layer**

</div>
