---
title: Building a Service – User Registration and Authentication
menu_order: 14
post_status: publish
post_excerpt: Step-by-step guide to building a real UserService with registration, login, JWTs, and validation.
taxonomy:
  category:
    - microservices
  post_tag:
    - user service
    - authentication
    - jwt
    - validation
    - express
    - mongodb
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Service Responsibilities](#service-responsibilities)
- [Tech Stack](#tech-stack)
- [Define the User Model](#define-the-user-model)
- [Setup Express + MongoDB](#setup-express--mongodb)
- [Implement Registration Endpoint](#implement-registration-endpoint)
- [Implement Login with JWT](#implement-login-with-jwt)
- [Basic Validation with Zod](#basic-validation-with-zod)
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

The `UserService` handles:

- ✅ User registration (name, email, password)
- ✅ Secure password hashing
- ✅ Login with JWT
- ✅ Token verification
- 🚫 Does _not_ handle authorization logic (e.g., roles, permissions)

---

## Tech Stack

- **Language**: TypeScript
- **Runtime**: Node.js
- **Framework**: Express
- **Database**: MongoDB (Mongoose)
- **Validation**: Zod
- **Auth**: JWT (jsonwebtoken)

---

## Define the User Model

```ts
// models/User.ts
import mongoose from "mongoose";

const UserSchema = new mongoose.Schema(
  {
    name: String,
    email: { type: String, unique: true },
    password: String,
  },
  { timestamps: true }
);

export default mongoose.model("User", UserSchema);
```

---

## Setup Express + MongoDB

```ts
// server.ts
import express from "express";
import mongoose from "mongoose";

const app = express();
app.use(express.json());

mongoose.connect(process.env.MONGO_URI || "mongodb://localhost/users");

app.listen(3000, () => console.log("UserService running on port 3000"));
```

---

## Implement Registration Endpoint

```ts
// routes/auth.ts
import express from "express";
import User from "../models/User";
import bcrypt from "bcrypt";

const router = express.Router();

router.post("/register", async (req, res) => {
  const { name, email, password } = req.body;

  const hash = await bcrypt.hash(password, 10);
  const user = await User.create({ name, email, password: hash });

  res.status(201).json({ id: user._id, email: user.email });
});

export default router;
```

---

## Implement Login with JWT

```ts
import jwt from "jsonwebtoken";

router.post("/login", async (req, res) => {
  const { email, password } = req.body;

  const user = await User.findOne({ email });
  if (!user || !(await bcrypt.compare(password, user.password))) {
    return res.status(401).json({ error: "Invalid credentials" });
  }

  const token = jwt.sign(
    { userId: user._id },
    process.env.JWT_SECRET || "secret",
    { expiresIn: "1h" }
  );
  res.json({ token });
});
```

---

## Basic Validation with Zod

```ts
import { z } from "zod";

const registerSchema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
  password: z.string().min(6),
});

router.post("/register", async (req, res) => {
  const result = registerSchema.safeParse(req.body);
  if (!result.success) {
    return res.status(400).json(result.error.format());
  }

  const { name, email, password } = result.data;
  // Continue with hashing + saving
});
```

---

## Summary

You've now built a real User Service with registration, login, hashing, JWT tokens, and Zod validation. This service can be reused by multiple frontend clients or other microservices.

---

Next:  
**Lesson 15 – Building Product and Inventory Services (with Event-Driven Updates)**

</div>
