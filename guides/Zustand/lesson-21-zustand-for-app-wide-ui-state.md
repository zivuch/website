---
title: Zustand for App-Wide UI State (Modals, Sidebars, Themes)
menu_order: 21
post_status: publish
post_excerpt: Learn how to use Zustand to manage global UI elements like modals, theme toggles, and sidebars.
taxonomy:
  category:
    - zustand
    - Practical Guide to Zustand
  post_tag:
    - zustand
    - ui state
    - modals
    - themes
    - react
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why UI State Belongs in Zustand
- Managing Modals Globally
- Sidebar and Drawer State
- Theme Toggle and Dark Mode
- Best Practices for Global UI Stores

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

## Why UI State Belongs in Zustand

Zustand is great for global UI state because:

- 📦 No Provider is needed
- 🎯 Easy to share state across layout and nested components
- 💡 Works well with modals, sidebars, themes, tooltips, etc.

---

## Managing Modals Globally

```ts
type ModalStore = {
  isOpen: boolean;
  openModal: () => void;
  closeModal: () => void;
};

export const useModalStore = create<ModalStore>((set) => ({
  isOpen: false,
  openModal: () => set({ isOpen: true }),
  closeModal: () => set({ isOpen: false }),
}));
```

In your modal component:

```tsx
const isOpen = useModalStore((s) => s.isOpen);
const closeModal = useModalStore((s) => s.closeModal);

{
  isOpen && <Modal onClose={closeModal} />;
}
```

Trigger globally:

```tsx
useModalStore.getState().openModal();
```

---

## Sidebar and Drawer State

```ts
type SidebarStore = {
  visible: boolean;
  toggle: () => void;
};

export const useSidebarStore = create<SidebarStore>((set) => ({
  visible: false,
  toggle: () => set((s) => ({ visible: !s.visible })),
}));
```

Works with a layout component or navbar button.

---

## Theme Toggle and Dark Mode

```ts
type ThemeStore = {
  darkMode: boolean;
  toggleTheme: () => void;
};

export const useThemeStore = create<ThemeStore>((set) => ({
  darkMode: false,
  toggleTheme: () => set((s) => ({ darkMode: !s.darkMode })),
}));
```

Update `document.body.classList` in `useEffect`:

```tsx
const darkMode = useThemeStore((s) => s.darkMode);

useEffect(() => {
  document.body.classList.toggle("dark", darkMode);
}, [darkMode]);
```

---

## Best Practices for Global UI Stores

✅ One store per feature (e.g., `useModalStore`, `useThemeStore`)  
✅ Avoid overloading one giant store with all UI  
✅ Persist theme preference if needed  
✅ Don’t use Zustand for **transient** component-local UI

---

## Summary

- Zustand is perfect for modals, sidebars, and themes
- Share state between layout and deeply nested components
- Keep stores focused and isolated by UI concern
- Avoid context hell for simple UI toggles

---

Next: **Lesson 22 – Combining Zustand with React Query for Async Data**

</div>
