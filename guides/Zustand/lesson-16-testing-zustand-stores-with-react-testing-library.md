---
title: Testing Zustand Stores with React Testing Library
menu_order: 16
post_status: publish
post_excerpt: Learn how to test Zustand stores and their interaction with React components using React Testing Library and Jest.
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - testing
    - react testing library
    - jest
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Test Zustand Stores?
- Testing Store Logic in Isolation
- Testing Store-Connected Components
- Mocking Zustand for Controlled State
- Cleanup and Best Practices

</div>

<div class="otg" markdown="1">

## On this Guide

- Lesson 09: Organizing State with Slices and Modular Stores
- Lesson 10: Persisting State to localStorage or sessionStorage
- Lesson 11: Using Devtools Middleware for Debugging
- Lesson 12: Using Zustand with Immer for Immutable Updates
- Lesson 13: Using Zustand with Middleware: Logging, Tracking, and Side Effects
- Lesson 14: Subscribing to External State Changes
- Lesson 15: Creating Read-Only or Transient State Stores
- Lesson 16: Testing Zustand Stores with React Testing Library
- Lesson 17: Using Zustand in Server-Side Rendering (Next.js)

</div>

</div>

<div class="guru-main" markdown="1">

## Why Test Zustand Stores?

Zustand is test-friendly because:

- ✅ No Provider required
- ✅ State is decoupled from UI
- ✅ You can access and mutate store outside components

---

## Testing Store Logic in Isolation

Stores can be tested like plain JavaScript:

```ts
import { useCounterStore } from "./store";

describe("Counter Store", () => {
  beforeEach(() => {
    useCounterStore.setState({ count: 0 });
  });

  it("increments count", () => {
    useCounterStore.getState().inc();
    expect(useCounterStore.getState().count).toBe(1);
  });

  it("resets count", () => {
    useCounterStore.setState({ count: 5 });
    useCounterStore.getState().reset();
    expect(useCounterStore.getState().count).toBe(0);
  });
});
```

Use `.setState()` and `.getState()` directly.

---

## Testing Store-Connected Components

Use **React Testing Library** to test components that read from Zustand:

```tsx
function CounterDisplay() {
  const count = useCounterStore((s) => s.count);
  return <div>{count}</div>;
}
```

Then in the test:

```ts
import { render, screen } from "@testing-library/react";

it("renders count from store", () => {
  useCounterStore.setState({ count: 42 });
  render(<CounterDisplay />);
  expect(screen.getByText("42")).toBeInTheDocument();
});
```

---

## Mocking Zustand for Controlled State

You can replace the store logic temporarily:

```ts
jest.mock("./store", () => ({
  useCounterStore: jest.fn(() => ({
    count: 99,
    inc: jest.fn(),
  })),
}));
```

This is useful when you want **pure UI tests** without actual state logic.

---

## Cleanup and Best Practices

✅ Always reset the store state after each test:

```ts
afterEach(() => {
  useCounterStore.setState({ count: 0 });
});
```

✅ Prefer `.getState()`/`.setState()` over firing events if testing store logic  
✅ For side effect testing (e.g., subscribe()), use mocks or spies

---

## Summary

- Zustand stores are easy to test in isolation or with UI
- Use `.setState()` and `.getState()` in tests
- Reset state between tests to avoid leaks
- Mock store logic for pure component rendering when needed

---

Next: **Lesson 17 – Using Zustand in Server-Side Rendering (Next.js)**

</div>
