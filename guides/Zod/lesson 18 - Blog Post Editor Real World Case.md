---
title: Real-World Case Study – Blog Post Editor Validation
menu_order: 18
post_status: publish
post_excerpt: Apply Zod in a real-world blog editor form with nested and conditional logic.
featured_image: _images/bg-p.png
taxonomy:
  category:
    - zod
    - Practical Guide
  post_tag:
    - blog editor
    - form validation
    - content rules
    - zod
---

<div class="toc" markdown="1">

## On this Page

- [The Scenario](#the-scenario)
- [Building the BlogPostSchema](#building-the-blogpostschema)
- [Handling Tags and Rich Content](#handling-tags-and-rich-content)
- [Validating Nested Metadata](#validating-nested-metadata)
- [Optional Draft Logic with Refinement](#optional-draft-logic-with-refinement)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## The Scenario

You're building a blog editor where authors submit the following data:

- `title`: required, min 5 chars
- `body`: required, min 50 chars
- `tags`: array of unique strings (1–5 items)
- `metadata`: includes `published`, `publishedAt`, and `slug`
- If `published` is `true`, `publishedAt` and `slug` must be set

Let’s build a robust schema for this.

---

## Building the `BlogPostSchema`

```ts
import { z } from "zod";

export const BlogPostSchema = z
  .object({
    title: z.string().min(5, "Title must be at least 5 characters"),
    body: z.string().min(50, "Content must be at least 50 characters"),
    tags: z
      .array(z.string().min(2))
      .min(1)
      .max(5)
      .refine((tags) => new Set(tags).size === tags.length, {
        message: "Tags must be unique",
      }),
    metadata: z.object({
      published: z.boolean(),
      publishedAt: z.string().optional(), // ISO string expected
      slug: z.string().optional(),
    }),
  })
  .superRefine((data, ctx) => {
    if (data.metadata.published) {
      if (!data.metadata.publishedAt) {
        ctx.addIssue({
          path: ["metadata", "publishedAt"],
          code: "custom",
          message: "Published date is required when published",
        });
      }

      if (!data.metadata.slug) {
        ctx.addIssue({
          path: ["metadata", "slug"],
          code: "custom",
          message: "Slug is required when published",
        });
      }
    }
  });
```

---

## Handling Tags and Rich Content

Zod lets you validate both structure and content:

```ts
tags: z
  .array(z.string().min(2, "Each tag must be at least 2 characters"))
  .min(1)
  .max(5)
```

Add `.refine()` to enforce uniqueness.

---

## Validating Nested Metadata

The `metadata` object is fully typed and validated:

```ts
metadata: z.object({
  published: z.boolean(),
  publishedAt: z.string().optional(),
  slug: z.string().optional(),
})
```

Use `.superRefine()` for cross-field logic like:
- If `published` is `true`, then both `publishedAt` and `slug` must be filled.

---

## Optional Draft Logic with Refinement

Want to allow drafts with just `title` and `body`?

```ts
if (!data.metadata.published) {
  // Allow missing `publishedAt` and `slug`
}
```

That’s the beauty of `.superRefine()` — you control the logic, not just the shape.

---

## Summary

- This schema combines strings, arrays, nested objects, optional fields, and cross-field rules
- Zod helps enforce business logic cleanly and predictably
- Perfect for CMS, editors, admin panels, or custom content tools

---

Next: **Lesson 19 – Zod + React Hook Form Integration for Full Form Validation**

---

*** Master the Code, Be the Guru! ***

</div>
