---
title: Zod + React Hook Form Integration for Full Form Validation
menu_order: 19
post_status: publish
taxonomy:
  category:
    - zod
  post_tag:
    - react hook form
    - form validation
    - react
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [Why Integrate Zod with React Hook Form?](#why-integrate-zod-with-react-hook-form)
- [Installing Required Packages](#installing-required-packages)
- [Creating the Zod Schema](#creating-the-zod-schema)
- [Connecting Zod to React Hook Form](#connecting-zod-to-react-hook-form)
- [Displaying Field Errors](#displaying-field-errors)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Integrate Zod with React Hook Form?

React Hook Form is one of the most popular form libraries in React — and Zod is the perfect pairing for it. Together, you get:

- ✅ Powerful form control & performance (React Hook Form)
- ✅ Type-safe, declarative validation (Zod)
- ✅ Automatic TypeScript inference
- ✅ Cleaner error handling

---

## Installing Required Packages

Install the required packages:

```bash
npm install react-hook-form @hookform/resolvers zod
```

---

## Creating the Zod Schema

```ts
import { z } from "zod";

export const LoginSchema = z.object({
  email: z.string().email("Invalid email"),
  password: z.string().min(6, "Password must be at least 6 characters"),
});

export type LoginInput = z.infer<typeof LoginSchema>;
```

---

## Connecting Zod to React Hook Form

```tsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { LoginSchema, LoginInput } from "@/schemas/login";

const LoginForm = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<LoginInput>({
    resolver: zodResolver(LoginSchema),
  });

  const onSubmit = (data: LoginInput) => {
    console.log("Form Data:", data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("email")} placeholder="Email" />
      {errors.email && <p>{errors.email.message}</p>}

      <input type="password" {...register("password")} placeholder="Password" />
      {errors.password && <p>{errors.password.message}</p>}

      <button type="submit">Login</button>
    </form>
  );
};
```

---

## Displaying Field Errors

React Hook Form automatically:
- Maps `ZodError` messages to your input fields
- Uses the same keys (`email`, `password`, etc.)
- Makes `errors.field.message` available for display

Simple and declarative:

```tsx
{errors.email && <p>{errors.email.message}</p>}
```

---

## Summary

- Use `zodResolver()` to plug Zod into React Hook Form
- Keep schemas reusable across frontend and backend
- Automatically handle validation + error display
- Combine type inference with validation for a safer DX

---

Next: **Lesson 20 – Final Thoughts, Best Practices, and Resources**

---

*** Master the Code, Be the Guru! ***

</div>
