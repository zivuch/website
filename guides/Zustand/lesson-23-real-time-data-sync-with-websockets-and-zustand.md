---
title: Real-Time Data Sync with WebSockets and Zustand
menu_order: 23
post_status: publish
post_excerpt: Learn how to sync Zustand store state in real time using WebSockets, sockets.io, or broadcast channels.
taxonomy:
  category:
    - zustand
    - Practical Guide to Zustand
  post_tag:
    - zustand
    - websockets
    - real-time
    - sync
    - socketio
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- Why Use Zustand for Real-Time State?
- Connecting WebSockets to Your Store
- Listening and Broadcasting Changes
- Handling Race Conditions
- Best Practices and Patterns

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

## Why Use Zustand for Real-Time State?

Zustand is a perfect fit for real-time apps:

- No context required — state is globally accessible
- Reactive updates from WebSocket listeners
- Stores can be updated by multiple sources

Perfect for:

- Chat apps
- Dashboards
- Multiplayer games
- Collaborative UIs

---

## Connecting WebSockets to Your Store

Create your WebSocket connection once (e.g., via Socket.IO or native):

```ts
const socket = io("wss://yourserver.com");

socket.on("connect", () => {
  console.log("Connected to WebSocket server");
});
```

Listen to incoming events:

```ts
socket.on("message", (msg) => {
  useChatStore.getState().addMessage(msg);
});
```

---

## Zustand Store Example

```ts
type ChatMessage = { id: string; user: string; text: string };

type ChatStore = {
  messages: ChatMessage[];
  addMessage: (msg: ChatMessage) => void;
};

export const useChatStore = create<ChatStore>((set) => ({
  messages: [],
  addMessage: (msg) => set((s) => ({ messages: [...s.messages, msg] })),
}));
```

---

## Broadcasting Changes

To send state changes back out:

```ts
const sendMessage = (text: string) => {
  const msg = { id: uuid(), user: "Me", text };
  useChatStore.getState().addMessage(msg);
  socket.emit("message", msg);
};
```

You can wrap this in a custom hook or service.

---

## Handling Race Conditions

🧠 Tips:

- Keep local state optimistic, then confirm via server
- Debounce rapid changes if needed
- Use timestamps or versioning if multiple users update the same data

---

## Best Practices and Patterns

✅ Centralize socket listeners (e.g., in a `useEffect` inside `_app.tsx`)  
✅ Use Zustand for shared UI + real-time data  
✅ Combine with other tools (e.g. React Query or RxJS if needed)  
✅ Unsubscribe and clean up on disconnect or unmount

---

## Summary

- Zustand works great with WebSockets and real-time updates
- Use `.getState()` to mutate on socket events
- Broadcast store changes via socket.emit()
- Ideal for live dashboards, chats, multiplayer UIs

---

Next: **Lesson 24 – Storing User Preferences and Settings**

</div>
