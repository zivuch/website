---
title: NestJS Project Structure and CLI
menu_order: 2
post_status: publish
post_excerpt: Learn how to scaffold, explore, and understand the file structure of a NestJS project using the powerful CLI.
taxonomy:
  category:
    - nestjs
    - Basic Guide to NestJS
  post_tag:
    - typescript
    - nestjs
    - cli
    - project-structure
    - scaffolding
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Installing the NestJS CLI](#installing-the-nestjs-cli)
- [Creating a New Project](#creating-a-new-project)
- [Project Folder Structure Overview](#project-folder-structure-overview)
- [What Each File and Folder Does](#what-each-file-and-folder-does)
- [Using the CLI to Generate Code](#using-the-cli-to-generate-code)
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

## Installing the NestJS CLI

NestJS comes with a powerful CLI that helps you scaffold and manage projects efficiently.

Install it globally:

```bash
npm install -g @nestjs/cli
```

Then check it's working:

```bash
nest --version
```

---

## Creating a New Project

Use the CLI to create your first project:

```bash
nest new my-app
```

You'll be prompted to choose a package manager (e.g., `npm`, `yarn`, or `pnpm`). Once complete, it sets up a fully working TypeScript project.

Start the server:

```bash
npm run start:dev
```

Visit [http://localhost:3000](http://localhost:3000) — you’ll see:  
`Hello World!`

---

## Project Folder Structure Overview

Here's what NestJS generates:

```
src/
  app.controller.ts
  app.service.ts
  app.module.ts
  main.ts
test/
  app.e2e-spec.ts
  jest-e2e.json
```

Also includes:

- `package.json`, `tsconfig.json`
- Lint, test, and start scripts
- Preconfigured testing setup with Jest

---

## What Each File and Folder Does

| File/Folders         | Purpose |
|----------------------|---------|
| `main.ts`            | Entry point – creates and runs the app |
| `app.module.ts`      | Root module – imports and wires all features |
| `app.controller.ts`  | Defines HTTP routes |
| `app.service.ts`     | Business logic provider |
| `test/`              | Contains auto-generated test scaffolding |
| `node_modules/`      | Your dependencies |
| `package.json`       | Scripts, metadata, and dependencies |
| `tsconfig.json`      | TypeScript config |

---

## Using the CLI to Generate Code

The CLI can generate modules, controllers, services, and more:

```bash
nest generate module users
nest generate controller users
nest generate service users
```

Or shorthand:

```bash
nest g mo users
nest g co users
nest g s users
```

It automatically updates `app.module.ts` to include new modules.

---

## Summary

The NestJS CLI gives you superpowers: it scaffolds new projects, follows best practices, and helps keep your codebase modular. You now understand how to create and navigate a NestJS app confidently.

> Next: **Lesson 03 – Modules, Controllers, and Providers**

</div>
