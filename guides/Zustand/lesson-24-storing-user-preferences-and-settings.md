---
title: Storing User Preferences and Settings
menu_order: 24
post_status: publish
post_excerpt: Learn how to store and persist user preferences like theme, language, and layout using Zustand.
taxonomy:
  category:
    - zustand
    - Practical Guide to Zustand
  post_tag:
    - zustand
    - preferences
    - settings
    - persist
    - user experience
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- What Are User Preferences?
- Structuring a Settings Store
- Persisting Preferences Across Sessions
- Syncing Preferences on Login
- Tips for Multi-User or Multi-Device Support

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

## What Are User Preferences?

User preferences include:

- Dark/light mode
- Language or locale
- Sidebar layout
- Grid or list view
- Font size or accessibility options

These are often user-specific and should be **persisted** across sessions.

---

## Structuring a Settings Store

```ts
import { create } from "zustand";
import { persist } from "zustand/middleware";

type SettingsStore = {
  darkMode: boolean;
  language: "en" | "he";
  toggleDarkMode: () => void;
  setLanguage: (lang: "en" | "he") => void;
};

export const useSettingsStore = create<SettingsStore>()(
  persist(
    (set) => ({
      darkMode: false,
      language: "en",
      toggleDarkMode: () => set((s) => ({ darkMode: !s.darkMode })),
      setLanguage: (lang) => set({ language: lang }),
    }),
    {
      name: "user-settings", // Key in localStorage
    }
  )
);
```

---

## Persisting Preferences Across Sessions

Zustand’s `persist` middleware stores preferences in `localStorage`:

```ts
persist(..., { name: "user-settings" })
```

✅ Values persist on page reload  
✅ Can also use `sessionStorage` or cookies

---

## Syncing Preferences on Login

If your backend saves user preferences:

```ts
// after login:
const serverSettings = await api.getUserPreferences();
useSettingsStore.setState(serverSettings);
```

This syncs server-stored settings into your local store.

You can also POST to save changes:

```ts
useEffect(() => {
  const settings = useSettingsStore.getState();
  api.saveUserPreferences(settings);
}, [language, darkMode]);
```

---

## Tips for Multi-User or Multi-Device Support

- Use a unique key per user if storing locally
- Sync preferences after login/logout
- Consider using a centralized API if preferences are shared between devices

```ts
persist(..., { name: `settings-${userId}` });
```

---

## Summary

- Use Zustand to manage app-wide user settings
- Persist settings using middleware
- Load or overwrite preferences from a backend
- Customize per-user storage keys if needed

---

Next: **Lesson 25 – Migrating from Redux or Context to Zustand**

</div>
