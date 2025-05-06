---
title: Setting Up TypeScript in Your Project
menu_order: 2
post_status: publish
post_excerpt: Learn how to install TypeScript, configure your project with tsconfig.json, and compile TypeScript to JavaScript.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - typescript
    - Basic Guide to TypeScript
  post_tag:
    - typescript
    - setup
    - configuration
    - tsconfig
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Installing TypeScript](#installing-typescript)
- [Creating a tsconfig.json File](#creating-a-tsconfigjson-file)
- [Basic Compiler Options](#basic-compiler-options)
- [Compiling TypeScript to JavaScript](#compiling-typescript-to-javascript)
- [Working with TypeScript in Node.js](#working-with-typescript-in-nodejs)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 01: What is TypeScript and Why Use It](./lesson-01-what-is-typescript-and-why-use-it)
- [Lesson 02: Setting Up TypeScript in Your Project](./lesson-02-setting-up-typescript-in-your-project)
- [Lesson 03: Basic Types and Type Annotations](./lesson-03-basic-types-and-type-annotations)
- [Lesson 04: Functions and Type Inference](./lesson-04-functions-and-type-inference)
- [Lesson 05: Objects, Interfaces, and Optional Properties](./lesson-05-objects,-interfaces,-and-optional-properties)

</div>

</div>

<div class="guru-main" markdown="1">

## Installing TypeScript

To use TypeScript, install it as a dev dependency in your project:

```bash
npm install typescript --save-dev
```

Or install globally:

```bash
npm install -g typescript
```

Then confirm it’s installed:

```bash
tsc --version
```

---

## Creating a `tsconfig.json` File

Run the following command to generate a base config:

```bash
npx tsc --init
```

This creates a `tsconfig.json` file which controls how TypeScript compiles your code.

---

## Basic Compiler Options

Here’s a minimal `tsconfig.json` for most projects:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "outDir": "dist",
    "rootDir": "src",
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["src"]
}
```

| Option         | Purpose                                        |
|----------------|------------------------------------------------|
| `strict`       | Enables all type-checking rules                |
| `esModuleInterop` | Allows `import x from 'y'` style imports     |
| `rootDir`/`outDir` | Control where your source and compiled files live |

---

## Compiling TypeScript to JavaScript

Place your `.ts` files in a `src/` folder, then run:

```bash
npx tsc
```

This compiles `.ts` files into `.js` in the `dist/` folder (or wherever you configured).

---

## Working with TypeScript in Node.js

Add this to `package.json`:

```json
"scripts": {
  "build": "tsc",
  "start": "node dist/index.js"
}
```

Use `ts-node` for quicker development:

```bash
npm install ts-node --save-dev
```

Run a file:

```bash
npx ts-node src/index.ts
```

---

## Summary

- Install TypeScript via npm
- Generate a `tsconfig.json` to control compilation
- Use `tsc` or `ts-node` to compile/run code
- Setup proper `src` and `dist` folders for clean separation

Next up: **basic types and how to annotate your variables like a pro.**

</div>
