---
title: Handling Booleans, Counters, and Simple Objects
menu_order: 5
post_status: publish
post_excerpt: Learn how to manage common UI patterns like toggles, counters, and simple objects using Zustand.
taxonomy:
  category:
    - zustand
    - Basic Guide to Zustand
  post_tag:
    - zustand
    - ui state
    - toggle
    - counters
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Managing Booleans with Toggle Actions
- Implementing a Counter Store
- Handling Small Object Updates
- Using Partial Set Updates

</div>

<div class="otg" markdown="1">

## On this Guide

- Lesson 01: Introduction to Zustand and Store Basics  
- Lesson 02: Creating Your First Store with TypeScript  
- Lesson 03: Reading and Updating State in React Components  
- Lesson 04: Selectors and Optimizing Renders  
- Lesson 05: Handling Booleans, Counters, and Simple Objects  
- Lesson 06: Derived State and Computed Values  
- Lesson 07: Type Inference and store typing best practices  
- Lesson 08: Custom Hooks and Reusable State Accessors  

</div>

</div>

<div class="guru-main" markdown="1">

## Managing Booleans with Toggle Actions

Toggles are a common UI need — dark mode, modals, sidebars, etc.

```ts
type ToggleStore = {
  isOpen: boolean;
  toggle: () => void;
};

const useToggleStore = create<ToggleStore>((set) => ({
  isOpen: false,
  toggle: () => set((state) => ({ isOpen: !state.isOpen })),
}));
```

You can now use:

```tsx
const isOpen = useToggleStore((s) => s.isOpen);
const toggle = useToggleStore((s) => s.toggle);
```

---

## Implementing a Counter Store

Counter patterns are ideal for understanding state mutation:

```ts
type CounterStore = {
  count: number;
  inc: () => void;
  dec: () => void;
  reset: () => void;
};

const useCounterStore = create<CounterStore>((set) => ({
  count: 0,
  inc: () => set((s) => ({ count: s.count + 1 })),
  dec: () => set((s) => ({ count: s.count - 1 })),
  reset: () => set({ count: 0 }),
}));
```

This pattern is fully reactive and easy to wire to UI buttons.

---

## Handling Small Object Updates

You can store simple object state like this:

```ts
type ProfileStore = {
  profile: {
    name: string;
    age: number;
  };
  updateProfile: (partial: Partial<{ name: string; age: number }>) => void;
};

const useProfileStore = create<ProfileStore>((set) => ({
  profile: { name: "", age: 0 },
  updateProfile: (partial) =>
    set((state) => ({
      profile: { ...state.profile, ...partial },
    })),
}));
```

```tsx
useProfileStore.getState().updateProfile({ name: "Ziv" });
```

---

## Using Partial Set Updates

When updating nested state, use spread operators to ensure **shallow merges**.

⚠️ Zustand’s `set()` does not deeply merge by default — you must do it manually or with Immer (later lesson).

---

## Summary

- Toggle and counter stores are great for UI logic
- Always spread nested objects manually when updating state
- Use actions like `toggle`, `inc`, `reset` for better clarity

---

Next: **Lesson 06 – Derived State and Computed Values**

</div>
