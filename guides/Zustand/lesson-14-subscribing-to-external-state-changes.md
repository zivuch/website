# Lesson 14

Content missing.---
title: Subscribing to External State Changes
menu_order: 14
post_status: publish
post_excerpt: Learn how to subscribe directly to Zustand store changes outside of React components for side effects or external sync.
taxonomy:
category: - zustand - Advanced Guide to Zustand
post_tag: - zustand - subscriptions - external state - effects

---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Subscribe Outside React?
- Using `.subscribe()` on a Store
- Example: Syncing to Local Storage
- Unsubscribing and Cleanup
- Best Practices and Pitfalls

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

## Why Subscribe Outside React?

Sometimes you need to run side effects **whenever a store changes**, even outside the React tree. Common use cases:

- Save data to `localStorage` manually
- Trigger analytics events
- Log transitions or track sessions

Zustand exposes a `.subscribe()` method for this.

---

## Using `.subscribe()` on a Store

You can subscribe to the **entire state**:

```ts
const unsub = useStore.subscribe((state) => {
  console.log("New state:", state);
});
```

Or subscribe to a **slice**:

```ts
const unsub = useStore.subscribe(
  (state) => state.count,
  (count, prevCount) => {
    console.log("Count changed:", prevCount, "→", count);
  }
);
```

This works **outside React**, including in `main.ts`, `useEffect()`, or Node contexts.

---

## Example: Syncing to Local Storage

```ts
useCounterStore.subscribe((state) => {
  localStorage.setItem("count", String(state.count));
});
```

This allows **manual persistence** for very specific cases, without using `persist()`.

---

## Unsubscribing and Cleanup

Store the returned function to clean up:

```ts
const unsub = useStore.subscribe(...);

unsub(); // stop listening
```

If used in `useEffect`, be sure to return it:

```ts
useEffect(() => {
  const unsub = useStore.subscribe(...);
  return unsub;
}, []);
```

---

## Best Practices and Pitfalls

✅ Use subscriptions for:

- Analytics
- Logging
- Manual persistence
- Live sync (WebSocket, Firebase)

🚫 Avoid:

- UI updates or state branching inside subscribers
- Mutating state in response to state (causes loops!)

---

## Summary

- Zustand supports external subscriptions to state
- Useful for non-UI side effects like analytics or persistence
- Always unsubscribe to avoid memory leaks
- Avoid doing complex state logic inside subscribers

---

Next: **Lesson 15 – Creating Read-Only or Transient State Stores**

</div>
