---
title: Introduction to CSS
menu_order: 1
post_status: publish
featured_image: ../../_images/bg-p.png
taxonomy:
  category:
    - css
  post_tag:
    - courses
---

<div class="toc" markdown="1">

## On this Page

- [What is CSS? Let's Break it Down!](#what-is-css)
- [The Core Ingredients: CSS Rules](#css-rules)
  - [The Selector: Targeting Your HTML](#selector)
  - [The Declaration Block: The Styling Instructions](#declaration-block)
- [How CSS Looks in Action: Rule Sets](#how-css-looks)
- [Important Tidbits: Semicolons, Formatting, and Keeping Things Tidy](#important-tidbits)
  - [The Mighty Semicolon](#the-mighty-semicolon)
  - [Formatting and Indentation: Making Your Code Human-Friendly](#formatting-and-indentation)
- [What's Next on Our CSS Adventure?](#whats-next)

</div>

<div class="guru-main" markdown="1">

## Introduction to CSS 

Hey there, future web designers! 👋 You've already taken the first step by wanting to learn about **CSS**. That's awesome! Think of CSS as the magic wand that lets you take plain HTML and make it look beautiful, organized, and just the way you want it.

In this first lesson, we're going to gently introduce you to what CSS is all about. We'll break down the basic building blocks so you can start to understand how it works its styling wonders. Don't worry if it sounds a bit technical at first – we'll use simple language and plenty of examples to make it crystal clear.

## What is CSS? Let's Break it Down! <a id="what-is-css"></a>

**CSS** stands for **Cascading Style Sheets**. Now, that might sound like a mouthful, but let's simplify it. Imagine you've built the structure of your website using **HTML** (think of it like the bare bones of a house). CSS is what you use to:

- **Style** the HTML elements: Change colors, fonts, sizes, and so much more.
- **Layout** your content: Decide where things should be positioned on the page (side-by-side, stacked, etc.).
- **Make your website responsive**: Ensure it looks good on different devices like phones, tablets, and desktops.

Think of it this way:

- **HTML** is the **content** and **structure** of your website.
- **CSS** is the **presentation** and **style** of your website.

While we're focusing on styling HTML in this tutorial, just so you know, CSS can actually be used to style other types of documents too!

## The Core Ingredients: CSS Rules <a id="css-rules"></a>

A CSS file isn't just a jumble of random instructions. It's organized into one or more **CSS rules**. Each rule tells the browser how to style specific HTML elements.

Every CSS rule has two main parts:

1.  **The Selector:** This is like pointing at the specific HTML element(s) you want to style. You tell CSS _which_ parts of your HTML the rule should apply to.
2.  **The Declaration Block:** This is where you put the actual styling instructions. It's enclosed in curly braces `{}` and contains one or more **declarations**.

Here's a visual representation:

```
/* This is a CSS rule */
selector {
  property: value; /* This is a declaration */
  another-property: another-value; /* Another declaration */
}
```

Let's dive deeper into these two key parts.

### The Selector: Targeting Your HTML <a id="selector"></a>

The **selector** is the first part of a CSS rule. It's like a specific address that helps you target the HTML elements you want to style. There are different ways to select elements, and we'll learn many of them later. For now, let's look at a simple example using an HTML tag name as a selector:

```css
p {
  color: blue;
}
```

In this example, `p` is the selector. It's telling the browser: "Hey, find all the `<p>` (paragraph) elements in my HTML file." The part inside the curly braces `{ color: blue; }` then says: "And make the text color of those paragraphs blue!"

Imagine your HTML looks like this:

```
<p>This is a paragraph of text.</p>
<p>Here's another paragraph!</p>
```

With the CSS rule above, both of these paragraphs will magically appear in blue in your web browser. Cool, right?

### The Declaration Block: The Styling Instructions <a id="declaration-block"></a>

The **declaration block** is the part of the CSS rule that's enclosed in curly braces `{}`. Inside this block, you'll find one or more **declarations**. Each declaration is a specific instruction on how to style the selected element(s).

A declaration consists of two things:

- **A Property:** This is the aspect you want to style (like `color`, `font-size`, `background-color`, etc.).
- **A Value:** This is the setting you want to apply to that property (like `blue`, `20px`, `yellow`, etc.).

And guess what? Each declaration ends with a semicolon (`;`). Think of it like a period at the end of a sentence.

Here's an example with a few declarations:

```css
h1 {
  color: green; /* Sets the text color to green */
  font-size: 36px; /* Sets the font size to 36 pixels */
  background-color: #f0f0f0; /* Sets the background color to a light gray */
}
```

This CSS rule selects all `<h1>` (heading 1) elements and applies three styles to them: green text, a large font size, and a light gray background.

## How CSS Looks in Action: Rule Sets <a id="how-css-looks"></a>

So, putting it all together, a CSS **rule set** has a **selector** and a **declaration block** containing one or more **declarations** (each with a **property** and a **value**).

Let's look at a few more examples to solidify this:

**Example 1: Styling a Link**

```css
a {
  color: purple;
}
```

Here, `a` is the selector (targeting all link elements), and `color: purple;` is the declaration, making the link text purple.

**Example 2: Styling Multiple Properties**

```css
div {
  border: 1px solid black; /* Adds a 1-pixel solid black border */
  padding: 10px; /* Adds 10 pixels of padding inside the element */
}
```

This rule selects all `<div>` elements and adds a border and some space inside them.

**Example 3: Targeting Multiple Elements with the Same Style**

Sometimes you want to apply the same styles to different elements. You can do this by listing the selectors separated by commas:

```css
h2,
h3 {
  text-align: center; /* Centers the text in all h2 and h3 headings */
  color: orange;
}
```

This rule will center the text and make it orange for all `<h2>` and `<h3>` headings.

**Example 4: Styling Based on Classes and IDs**

As we mentioned earlier, you can also target elements using their `class` and `id` attributes in HTML.

- **Classes:** Used to group elements and apply the same styles. Class selectors start with a dot (`.`).

  ```css
  .important-text {
    font-weight: bold; /* Makes the text bold for all elements with the class "important-text" */
  }
  ```

  In your HTML:

  ```html
  <p class="important-text">This is important!</p>
  <div>This is <span class="important-text">also</span> important.</div>
  ```

- **IDs:** Used to uniquely identify a single element on the page. ID selectors start with a hash symbol (`#`).

  ```css
  #website-title {
    font-size: 48px; /* Makes the font size of the element with the ID "website-title" very large */
  }
  ```

  In your HTML:

  ```
  <h1 id="website-title">My Awesome Website</h1>
  ```

We'll explore these powerful selectors in much more detail in a future lesson!

## Important Tidbits: Semicolons, Formatting, and Keeping Things Tidy <a id="important-tidbits"></a>

### The Mighty Semicolon <a id="the-mighty-semicolon"></a>

Remember that little semicolon (`;`) at the end of each declaration? It's super important! It tells the browser where one style instruction ends and the next one begins. While it might seem optional after the very last declaration in a rule, it's a good habit to always include it. This helps prevent errors if you decide to add more styles later.

**Good Practice:**

```css
p {
  color: red;
  font-size: 16px; /* Always end with a semicolon */
}
```

**Potential Trouble:**

```css
p {
  color: red;
  font-size: 16px; /* Oops, missing a semicolon! */
}
```

### Formatting and Indentation: Making Your Code Human-Friendly <a id="formatting-and-indentation"></a>

The browser doesn't really care how you format your CSS code as long as it's correct. However, _you_ and other developers who might work with your code later will definitely appreciate it if your code is well-formatted and easy to read.

This CSS is valid but looks like a jumbled mess:

```css
body {
  background-color: white;
}
h1 {
  color: blue;
  font-size: 2em;
}
p {
  line-height: 1.5;
}
```

Instead, aim for a clear and consistent style like this:

```css
body {
  background-color: white;
}

h1 {
  color: blue;
  font-size: 2em;
}

p {
  line-height: 1.5;
}
```

Here are some common formatting conventions:

- Put the opening curly brace `{` on the same line as the selector, with a space before it.
- Indent the declarations inside the curly braces (usually by 2 or 4 spaces).
- Put each property-value pair on its own line.
- Always end each declaration with a semicolon `;`.
- Put the closing curly brace `}` on a new line, aligned with the selector.

Consistent formatting makes your CSS much easier to understand, debug, and maintain. It's like writing neatly – it just makes everything clearer!

## What's Next on Our CSS Adventure? <a id="whats-next"></a>

Fantastic! You've now taken your first steps into the world of CSS. You understand the basic structure of CSS rules, selectors, and declarations. You also know why it's important to use semicolons and good formatting.

In our next lessons, we'll explore:

- **How to actually link your CSS to your HTML files** (there are a few ways to do this!).
- **Different types of selectors** in more detail, so you can target exactly the elements you want.
- **Some fundamental CSS properties** that will allow you to change text, colors, and backgrounds.

Keep playing around with the examples and don't be afraid to experiment. The more you practice, the more intuitive CSS will become. Get ready to unleash your creativity and make your web pages shine! ✨

Master the Code, Be the Guru!

</div>
