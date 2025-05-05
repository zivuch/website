---
title: Combining Zustand with React Query for Async Data
menu_order: 22
post_status: publish
post_excerpt: Learn how to integrate Zustand with React Query to manage global async data alongside local state.
taxonomy:
  category:
    - zustand
    - Practical Guide to Zustand
  post_tag:
    - zustand
    - react query
    - async
    - data fetching
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Combine Zustand and React Query?
- What Goes in Each Tool?
- Sharing Fetched Data via Zustand
- Mutations and Cache Syncing
- Example Architecture

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

## Why Combine Zustand and React Query?

React Query is great for:

- ✅ Server cache
- ✅ Async fetch lifecycle
- ✅ Background refetching

Zustand is great for:

- ✅ Local UI state
- ✅ Global flags (loading, auth)
- ✅ Custom derivations and app-specific logic

You can **use them together** — and many teams do!

---

## What Goes in Each Tool?

| State Type         | Tool               |
| ------------------ | ------------------ |
| User token, modals | Zustand            |
| Fetched posts      | React Query        |
| Sidebar toggle     | Zustand            |
| API error overlays | Zustand            |
| Search filters     | Zustand (optional) |
| Mutation response  | React Query        |

---

## Sharing Fetched Data via Zustand

You can fetch with React Query and sync it into Zustand:

```ts
const { data } = useQuery(["posts"], fetchPosts);

useEffect(() => {
  if (data) usePostStore.getState().setPosts(data);
}, [data]);
```

Now Zustand holds the same list — for reactivity across pages.

---

## Mutations and Cache Syncing

After a mutation, you can:

1. Invalidate the query:

```ts
await mutateAsync();
queryClient.invalidateQueries(["posts"]);
```

2. Or push the updated item into Zustand:

```ts
usePostStore.getState().addPost(newPost);
```

You can even subscribe to query updates in Zustand using `.subscribe()` if needed.

---

## Example Architecture

```ts
// React Query for fetches/mutations
// Zustand for UI state and selection

const { data } = useQuery(["posts"], fetchPosts);

useEffect(() => {
  useUIStore.getState().setLoading(false);
}, [data]);
```

Zustand handles:

- Selection
- Modal open/close
- Filtering UI
- Current tab

React Query handles:

- Fetching + caching
- Retry/fail logic
- Background polling

---

## Summary

- Use Zustand for UI, local/global flags, and selection
- Use React Query for async data and API interaction
- You can sync them for shared workflows
- Keep responsibilities separate for clarity and performance

---

Next: **Lesson 23 – Real-Time Data Sync with WebSockets and Zustand**

</div>
