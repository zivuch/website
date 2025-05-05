---
title: Creating Read-Only or Transient State Stores
menu_order: 15
post_status: publish
post_excerpt: Learn how to define state stores that are either temporary or strictly read-only for better architecture and control.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zustand
    - Advanced Guide to Zustand
  post_tag:
    - zustand
    - readonly
    - ephemeral
    - transient
    - architecture
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What Is a Transient or Read-Only Store?
- Read-Only Store Pattern
- Volatile State (Ephemeral Data)
- Best Use Cases
- Limitations and Alternatives

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

## What Is a Transient or Read-Only Store?

Sometimes you need a Zustand store that:

- Is **read-only** (state is set internally, not from UI)
- Is **transient** (used only during a session or interaction)
- Has **volatile** state (cleared when the tab closes or user logs out)

These are useful in **modular apps**, **step forms**, or **streaming UIs**.

---

## Read-Only Store Pattern

Make a store that doesn’t expose mutators:

```ts
type AppMetaStore = {
  version: string;
  build: string;
};

export const useAppMetaStore = create<AppMetaStore>(() => ({
  version: "1.2.3",
  build: "production",
}));
```

Consumers can read:

```ts
const version = useAppMetaStore((s) => s.version);
```

But cannot update it — no `set()` is exposed.

---

## Volatile State (Ephemeral Data)

Use Zustand for temporary state like:

- Drag-and-drop targets
- Unsaved form fields
- Modals or tooltips
- Selection in a grid/table

These stores reset easily:

```ts
type HoverState = {
  hoveredId: string | null;
  setHovered: (id: string | null) => void;
};

export const useHoverStore = create<HoverState>((set) => ({
  hoveredId: null,
  setHovered: (id) => set({ hoveredId: id }),
}));
```

Reset the store on `onMouseLeave`, for example.

---

## Best Use Cases

✅ Read-only stores:

- Version metadata
- App config (from `.env`)
- SSR-injected context

✅ Transient stores:

- UI interaction (hover, drag)
- Forms in progress
- Onboarding steps

---

## Limitations and Alternatives

- Zustand doesn’t have a built-in way to lock write access — it’s a convention
- Use `readonly` types or only export derived selectors if needed

Alternative approach: create a read-only hook

```ts
export const useAppVersion = () => useAppMetaStore((s) => s.version);
```

---

## Summary

- Zustand can support both read-only and short-lived state stores
- Useful for app metadata, UI state, and flow control
- Use conventions to restrict mutation
- Don’t overcomplicate — keep it simple and local if possible

---

Next: **Lesson 16 – Testing Zustand Stores with React Testing Library**

</div>
