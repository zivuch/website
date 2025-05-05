---
title: Zustand for Authentication and Session Management
menu_order: 18
post_status: publish
post_excerpt: Learn how to use Zustand to manage auth tokens, user info, and session state across your app.
taxonomy:
  category:
    - zustand
    - Practical Guide to Zustand
  post_tag:
    - zustand
    - authentication
    - session
    - login
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Use Zustand for Auth?
- Managing Tokens and User Info
- Handling Login and Logout
- Persisting Sessions Safely
- Accessing Auth State in Components

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

## Why Use Zustand for Auth?

Zustand is ideal for auth because:

- ✅ Global access to auth state from any component
- ✅ No need for providers or context
- ✅ Easy integration with localStorage or cookies
- ✅ One store handles both logic and reactive access

---

## Managing Tokens and User Info

Here’s a simple auth store:

```ts
import { create } from "zustand";
import { persist } from "zustand/middleware";

type AuthStore = {
  user: null | { id: string; name: string };
  token: string | null;
  login: (user: { id: string; name: string }, token: string) => void;
  logout: () => void;
};

export const useAuthStore = create<AuthStore>()(
  persist(
    (set) => ({
      user: null,
      token: null,
      login: (user, token) => set({ user, token }),
      logout: () => set({ user: null, token: null }),
    }),
    {
      name: "auth-store", // localStorage key
    }
  )
);
```

---

## Handling Login and Logout

In your auth service:

```ts
// Login function
async function handleLogin(email: string, password: string) {
  const { token, user } = await api.login(email, password);
  useAuthStore.getState().login(user, token);
}

// Logout function
function handleLogout() {
  useAuthStore.getState().logout();
}
```

This works from any component, service, or route handler.

---

## Persisting Sessions Safely

Zustand’s `persist` middleware keeps the token in `localStorage`:

```ts
{
  name: "auth-store",
  partialize: (state) => ({ user: state.user, token: state.token })
}
```

If you're using sensitive tokens, you may prefer `sessionStorage` or secure cookies.

You can also define a custom storage backend:

```ts
storage: {
  getItem: (key) => sessionStorage.getItem(key),
  setItem: (key, value) => sessionStorage.setItem(key, value),
  removeItem: (key) => sessionStorage.removeItem(key),
}
```

---

## Accessing Auth State in Components

```tsx
const user = useAuthStore((s) => s.user);
const token = useAuthStore((s) => s.token);
```

Use actions:

```tsx
const logout = useAuthStore((s) => s.logout);
<button onClick={logout}>Log Out</button>;
```

---

## Summary

- Zustand makes managing auth state simple and centralized
- You can store and persist user info + tokens
- Auth logic can live outside the UI and be shared app-wide
- Customize storage and structure to fit your security needs

---

Next: **Lesson 19 – Managing Forms and Multi-Step Wizards with Zustand**

</div>
