---
title: Undo/Redo Functionality with State Snapshots
menu_order: 20
post_status: publish
post_excerpt: Learn how to implement undo and redo functionality in Zustand using simple history tracking and snapshots.
taxonomy:
  category:
    - zustand
    - Practical Guide to Zustand
  post_tag:
    - zustand
    - undo
    - redo
    - snapshots
    - history
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Snapshots Matter
- Storing History in Zustand
- Implementing Undo and Redo Logic
- Edge Cases and State Limits
- UI Integration Example

</div>

<div class="otg" markdown="1">

## On this Guide

- Lesson 18: Zustand for Authentication and Session Management
- Lesson 19: Managing Forms and Multi-Step Wizards with Zustand
- Lesson 20: Undo/Redo Functionality with State Snapshots
- Lesson 21: Zustand for App-Wide UI State (Modals, Sidebars, Themes)
- Lesson 22: Combining Zustand with React Query for Async Data
- Lesson 23: Real-Time Data Sync with WebSockets and Zustand
- Lesson 24: Storing User Preferences and Settings
- Lesson 25: Migrating from Redux or Context to Zustand

</div>

</div>

<div class="guru-main" markdown="1">

## Why Snapshots Matter

Undo/redo is a common UX feature in:

- Text editors
- Drawing apps
- Form wizards
- Workflow builders

Zustand doesn’t include this by default — but we can build it!

---

## Storing History in Zustand

We'll store a stack of state snapshots manually:

```ts
import { create } from "zustand";

type HistoryState<T> = {
  past: T[];
  present: T;
  future: T[];
  set: (newState: T) => void;
  undo: () => void;
  redo: () => void;
};

export const useHistoryStore = create<HistoryState<number>>((set, get) => ({
  past: [],
  present: 0,
  future: [],
  set: (newState) => {
    const { past, present } = get();
    set({
      past: [...past, present],
      present: newState,
      future: [],
    });
  },
  undo: () => {
    const { past, present, future } = get();
    if (past.length === 0) return;
    const previous = past[past.length - 1];
    const newPast = past.slice(0, past.length - 1);
    set({
      past: newPast,
      present: previous,
      future: [present, ...future],
    });
  },
  redo: () => {
    const { past, present, future } = get();
    if (future.length === 0) return;
    const next = future[0];
    const newFuture = future.slice(1);
    set({
      past: [...past, present],
      present: next,
      future: newFuture,
    });
  },
}));
```

You can use `number`, an object, or any other type as the snapshot value.

---

## Implementing Undo and Redo Logic

```tsx
const value = useHistoryStore((s) => s.present);
const undo = useHistoryStore((s) => s.undo);
const redo = useHistoryStore((s) => s.redo);

<button onClick={undo}>Undo</button>
<button onClick={redo}>Redo</button>
```

Updating the value:

```tsx
useHistoryStore.getState().set(value + 1);
```

---

## Edge Cases and State Limits

- 🧠 Add a `maxHistory` limit if needed
- 🧼 Clear history after save/submit
- 🚫 Prevent duplicate `present` values if no change occurred

---

## UI Integration Example

```tsx
function Counter() {
  const value = useHistoryStore((s) => s.present);
  return <div>Current: {value}</div>;
}
```

This pattern can apply to:

- Canvas editors (track objects drawn)
- Form drafts (step-by-step undo)
- JSON builders and UI designers

---

## Summary

- Zustand can power undo/redo with manual history stacks
- Track `past`, `present`, and `future` states
- Keep logic in the store and trigger from the UI
- Add limits and edge case handling for better UX

---

Next: **Lesson 21 – Zustand for App-Wide UI State (Modals, Sidebars, Themes)**

</div>
