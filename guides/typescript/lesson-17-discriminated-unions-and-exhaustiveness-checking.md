---
title: Using TypeScript with Node.js and Express
menu_order: 17
post_status: publish
post_excerpt: Learn how to use TypeScript with Node.js and Express to write robust, type-safe APIs with minimal effort.
taxonomy:
  category:
    - typescript
    - Practical Guide to TypeScript
  post_tag:
    - typescript
    - nodejs
    - express
    - backend
    - api
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Setting Up TypeScript in a Node Project](#setting-up-typescript-in-a-node-project)
- [Installing Express with Type Support](#installing-express-with-type-support)
- [Creating a Basic Express Server](#creating-a-basic-express-server)
- [Typing Request and Response Objects](#typing-request-and-response-objects)
- [Defining Request Body and Params Types](#defining-request-body-and-params-types)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 16: Using TypeScript in a React Project](./lesson-16-using-typescript-in-a-react-project)
- [Lesson 17: Using TypeScript with Node.js and Express](./lesson-17-using-typescript-with-nodejs-and-express)
- [Lesson 18: Defining API Schemas with Zod and TypeScript](./lesson-18-defining-api-schemas-with-zod-and-typescript)
- [Lesson 19: Integrating TypeScript with Zustand or Redux](./lesson-19-integrating-typescript-with-zustand-or-redux)

</div>

</div>

<div class="guru-main" markdown="1">

## Setting Up TypeScript in a Node Project

```bash
npm init -y
npm install typescript ts-node-dev --save-dev
npx tsc --init
```

Enable these options in `tsconfig.json`:

```json
"esModuleInterop": true,
"strict": true,
"rootDir": "src",
"outDir": "dist"
```

---

## Installing Express with Type Support

```bash
npm install express
npm install --save-dev @types/express
```

Create a folder called `src/` and add your server file there.

---

## Creating a Basic Express Server

```ts
// src/index.ts
import express from "express";

const app = express();
app.use(express.json());

app.get("/", (req, res) => {
  res.send("Hello from TypeScript + Express!");
});

app.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
```

Run with:

```bash
npx ts-node-dev src/index.ts
```

---

## Typing Request and Response Objects

You can add types from Express:

```ts
import { Request, Response } from "express";

app.get("/user", (req: Request, res: Response) => {
  res.json({ name: "Lior" });
});
```

---

## Defining Request Body and Params Types

Type your API like you would a function:

```ts
type User = {
  name: string;
  age: number;
};

app.post("/users", (req: Request<{}, {}, User>, res: Response) => {
  const user = req.body; // Fully typed
  res.status(201).json(user);
});
```

You can also type `req.params` and `req.query`:

```ts
app.get("/user/:id", (req: Request<{ id: string }>, res: Response) => {
  const { id } = req.params;
  res.send(`User ID: ${id}`);
});
```

---

## Summary

- TypeScript + Express = fast and safe backend APIs
- Use `ts-node-dev` for live-reloading
- Use generics in `Request<Params, ResBody, ReqBody>` for full typing
- Clean up logic with interfaces, validation, and middleware

Next up: **Lesson 18 – Defining API Schemas with Zod and TypeScript**

</div>
