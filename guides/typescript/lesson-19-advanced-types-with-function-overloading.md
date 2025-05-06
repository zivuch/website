---
title: Integrating TypeScript with Zustand or Redux
menu_order: 19
post_status: publish
post_excerpt: Learn how to use TypeScript with Zustand or Redux for safe and scalable global state management in React apps.
taxonomy:
  category:
    - typescript
    - Practical Guide to TypeScript
  post_tag:
    - typescript
    - zustand
    - redux
    - state management
    - react
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Use TypeScript in State Management](#why-use-typescript-in-state-management)
- [Using TypeScript with Zustand](#using-typescript-with-zustand)
- [Creating a Typed Zustand Store](#creating-a-typed-zustand-store)
- [Using TypeScript with Redux Toolkit](#using-typescript-with-redux-toolkit)
- [Typing Redux Slices and Selectors](#typing-redux-slices-and-selectors)
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

## Why Use TypeScript in State Management

Using TypeScript with your state management solution:

- Prevents silent bugs from mistyped property names
- Helps you refactor code safely
- Improves auto-completion in IDEs
- Brings structure to growing apps

---

## Using TypeScript with Zustand

Install Zustand:

```bash
npm install zustand
```

---

## Creating a Typed Zustand Store

```ts
import { create } from "zustand";

type BearState = {
  count: number;
  increase: () => void;
};

const useBearStore = create<BearState>((set) => ({
  count: 0,
  increase: () => set((state) => ({ count: state.count + 1 }))
}));

// In your component:
const count = useBearStore((s) => s.count);
```

Zustand’s API is simple and works **beautifully with TypeScript**.

---

## Using TypeScript with Redux Toolkit

Install Redux Toolkit and types:

```bash
npm install @reduxjs/toolkit react-redux
npm install --save-dev @types/react-redux
```

Create a slice with typed state:

```ts
import { createSlice, PayloadAction } from "@reduxjs/toolkit";

interface CounterState {
  value: number;
}

const initialState: CounterState = { value: 0 };

const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment(state) {
      state.value++;
    },
    addBy(state, action: PayloadAction<number>) {
      state.value += action.payload;
    }
  }
});

export const { increment, addBy } = counterSlice.actions;
export default counterSlice.reducer;
```

---

## Typing Redux Slices and Selectors

In `store.ts`:

```ts
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

export const store = configureStore({
  reducer: {
    counter: counterReducer
  }
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```

In components:

```ts
import { useSelector, useDispatch } from "react-redux";
import type { RootState, AppDispatch } from "./store";

const value = useSelector((state: RootState) => state.counter.value);
const dispatch = useDispatch<AppDispatch>();
```

---

## Summary

- Zustand and Redux Toolkit both work great with TypeScript
- Zustand: use generic typing on store creation
- Redux Toolkit: type state, payloads, selectors, and dispatch
- State management becomes **predictable and safe** with TypeScript

Next up: **Lesson 20 – Final Thoughts, Best Practices, and Resources**

</div>
