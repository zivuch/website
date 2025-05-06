---
title: Using TypeScript in a React Project
menu_order: 16
post_status: publish
post_excerpt: Learn how to use TypeScript in a React project to safely type props, state, and components with confidence.
taxonomy:
  category:
    - typescript
    - Practical Guide to TypeScript
  post_tag:
    - typescript
    - react
    - props
    - component types
    - hooks
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Creating a React App with TypeScript](#creating-a-react-app-with-typescript)
- [Typing Component Props](#typing-component-props)
- [Typing Component State](#typing-component-state)
- [Typing Events and Refs](#typing-events-and-refs)
- [Using TypeScript with Hooks](#using-typescript-with-hooks)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 16: Using TypeScript in a React Project](./lesson-16-using-typescript-in-a-react-project)
- [Lesson 17: Using TypeScript with Node.js and Express](./lesson-17-using-typescript-with-nodejs-and-express)
- [Lesson 18: Defining API Schemas with Zod and TypeScript](./lesson-18-defining-api-schemas-with-zod-and-typescript)
- [Lesson 19: Integrating TypeScript with Zustand or Redux](./lesson-19-integrating-typescript-with-zustand-or-redux)

</div>

</div>

<div class="guru-main" markdown="1">

## Creating a React App with TypeScript

Use `create-react-app` with the TypeScript template:

```bash
npx create-react-app my-app --template typescript
```

Or if using Vite:

```bash
npm create vite@latest my-app -- --template react-ts
```

---

## Typing Component Props

```tsx
type GreetingProps = {
  name: string;
  age?: number;
};

const Greeting: React.FC<GreetingProps> = ({ name, age }) => (
  <h2>
    Hello, {name}! {age && `You are ${age} years old.`}
  </h2>
);
```

- `age` is optional.
- Props are fully type-checked.

---

## Typing Component State

```tsx
const [count, setCount] = useState<number>(0);
```

You can omit the type if the initial value provides a clear inference:

```tsx
const [text, setText] = useState("Hello"); // inferred as string
```

---

## Typing Events and Refs

```tsx
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  console.log(e.target.value);
};

const inputRef = useRef<HTMLInputElement>(null);
```

React provides event types and DOM references for most use cases.

---

## Using TypeScript with Hooks

### useReducer:

```ts
type Action = { type: "increment" } | { type: "decrement" };
type State = { count: number };

function reducer(state: State, action: Action): State {
  switch (action.type) {
    case "increment": return { count: state.count + 1 };
    case "decrement": return { count: state.count - 1 };
  }
}

const [state, dispatch] = useReducer(reducer, { count: 0 });
```

### useContext:

Define types for context values:

```tsx
type Theme = "light" | "dark";

const ThemeContext = createContext<Theme>("light");

const theme = useContext(ThemeContext);
```

---

## Summary

- Use `React.FC<Props>` or typed props directly in function components
- Type `useState`, `useReducer`, `useContext`, and DOM events for safety
- TypeScript brings **clarity, safety, and auto-complete** to React apps
- Build your components like building an API — with strict contracts

Next up: **Lesson 17 – Using TypeScript with Node.js and Express**.

</div>
