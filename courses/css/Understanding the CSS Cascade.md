---
title: Understanding the CSS Cascade
menu_order: 5
post_status: publish
taxonomy:
  category:
    - css
  post_tag:
    - courses
---

<div class="toc" markdown="1">

## On this Page

- [What is the Cascade?](#what-is-the-cascade)
- [Key Factors in the Cascade](#key-factors)
  - [Position and Order of Appearance](#position-and-order)
  - [Specificity: How Selectors Compete](#specificity)
  - [Origin: Where Styles Come From](#origin)
  - [Importance: The `!important` Rule](#importance)
- [Putting it All Together](#putting-it-all-together)
- [Why the Cascade Matters](#why-the-cascade-matters)

</div>

<div class="main" markdown="1">

# Understanding the CSS Cascade: Resolving Style Conflicts

**Cascade** is a core concept in CSS. In fact, it's so important that it's right there in the name: **Cascading Style Sheets**. But what exactly does "cascading" mean in this context?

## What is the Cascade? <a id="what-is-the-cascade"></a>

The cascade is the set of rules that the browser uses to decide which CSS styles to apply to an HTML element when multiple conflicting CSS rules could potentially apply. It's like a referee that resolves disagreements between different style instructions.

Imagine you're telling your browser to style a button. You might have one rule that says "make it red" and another that says "make it blue." The cascade is what determines which color the button _actually_ ends up being.

The cascade considers several factors to make its decision, including:

- **Specificity:** How precisely the CSS selector targets the element.
- **Origin:** Where the CSS rules come from (e.g., your stylesheet, the browser's default styles).
- **Order:** The order in which the CSS rules appear in your code.
- **Importance:** The use of the `!important` declaration.
- **Inheritance:** Some CSS properties are inherited from parent elements.

## Key Factors in the Cascade <a id="key-factors"></a>

Let's break down these factors one by one.

### Position and Order of Appearance <a id="position-and-order"></a>

The order in which your CSS rules are defined matters. If two rules have the same specificity and origin, the rule that appears _later_ in the CSS will take precedence.

**Example:**

```css
button {
  color: red; /* First rule */
}

button {
  color: blue; /* Second rule */
}
```

If these rules are applied to a `<button>` element, the text will be **blue** because the `color: blue;` rule comes later.

This also applies to how you include your CSS:

- Styles defined in a `<link>` tag that comes later in the `<head>` will generally override styles in earlier `<link>` tags.
- Styles within a `<style>` tag declared later in the `<head>` or even in the `<body>` will generally override styles in `<link>` tags declared earlier in the `<head>`.
- Inline styles (defined directly in the HTML `style` attribute) generally override styles defined in `<style>` tags or `<link>` tags.

**Important Note:** The `!important` rule (which we'll discuss later) can override this order.

### Specificity: How Selectors Compete <a id="specificity"></a>

Specificity is a way of weighting CSS selectors to determine which rule is more precise and therefore should be applied. Some selectors are more specific than others.

Here's a simplified way to think about specificity:

- **IDs are very specific:** `#my-element` is more specific than anything else that targets the same element.
- **Classes are more specific than element selectors:** `.my-class` is more specific than `div`.
- **Element selectors are the least specific:** `div` is less specific than anything else.

**Example:**




```css
div {
  color: blue; /** Least specific */
}

.my-container .text {
  color: green; /** More specific */
}

#my-div .text {
  color: orange; /** Even more specific */
}

#my-div {
  color: red; /** This only affects the div itself */
}
```

In this case, the paragraph element (`<p class="text">`) will have **orange** text because the `#my-div .text` selector is the most specific.

We'll have a dedicated lesson on specificity later because it's a crucial part of understanding how CSS works\!

### Origin: Where Styles Come From <a id="origin"></a>

The origin of CSS rules also plays a role in the cascade. CSS rules can come from different sources:

1.  **User agent styles:** These are the default styles applied by the browser itself. Every browser has its own built-in stylesheet that provides basic styling for HTML elements. This is why headings are bold and links are blue by default.
2.  **User styles:** These are styles defined by the user of the browser, often through browser extensions or operating system settings. For example, a user might set a default font size for all web pages.
3.  **Author styles:** These are the styles that you, the web developer, write in your CSS files.

**The order of importance (from least to most important) is generally:**

1.  User agent styles
2.  User styles
3.  Author styles

This means that your CSS (author styles) will generally override the browser's default styles (user agent styles), and user styles will override author styles, except when using `!important`.

### Importance: The `!important` Rule <a id="importance"></a>

The `!important` rule is a way to give a CSS declaration higher priority in the cascade. It essentially says, "This style is very important, and it should override any other conflicting styles."

**Example:**

```css
button {
  color: red !important;
}

button {
  color: blue;
}
```

Even though the `color: blue;` rule comes later, the button's text will be **red** because of the `!important` declaration.

**Use `!important` sparingly!** Overusing it can make your CSS harder to understand and maintain, as it breaks the normal cascade flow. It's generally best to rely on specificity and order to control your styles.

## Putting it All Together <a id="putting-it-all-together"></a>

When the browser is trying to determine which style to apply to an element, it goes through the cascade algorithm, considering all the factors we've discussed:

1.  It collects all the CSS rules that apply to that element.
2.  It sorts the rules by origin (user agent, user, author).
3.  Within each origin, it sorts the rules by specificity.
4.  If there are still conflicts, it sorts by order of appearance.
5.  Finally, it considers `!important` declarations, which can override everything else.

## Why the Cascade Matters <a id="why-the-cascade-matters"></a>

Understanding the cascade is essential for writing effective CSS. It helps you:

- **Control the styling of your web pages:** You can predict which styles will be applied and avoid unexpected results.
- **Debug CSS issues:** When styles don't look the way you expect, you can use your knowledge of the cascade to figure out why.
- **Write maintainable CSS:** By using specificity and `!important` appropriately, you can create CSS that is easier to update and modify.

In the next lesson, we'll take a closer look at specificity, which is a key part of the cascade.

</div>
