---
title: A Brief History of CSS
menu_order: 2
post_status: publish
featured_image: ../../_images/bg-p.png
taxonomy:
  category:
    - css
  post_tag:
    - courses
---

<div class="toc" markdown="1">

## On this lesson

- [The "Academic" Web and the Need for Style](#the-academic-web)
- [The Inline Styling Era (and Why It Didn't Last)](#inline-styling)
- [The Birth of CSS: Separating Structure from Style](#birth-of-css)
- [CSS is Always Evolving](#css-evolving)
- [A Look Back at the Browser Wars](#browser-wars)
- [The Realization: We Need a Standard!](#need-for-standard)
- [The Birth of CSS Levels](#css-levels)
- [Browser Implementation: A Bit of a Rocky Start](#browser-implementation)
- [Where We Are Today: A Much Brighter Styling Landscape](#css-today)
- [Key Takeaway](#key-takeaway)

</div>

<div class="guru-main" markdown="1">

## A Quick Look Back: The Story of CSS

Before we dive deeper into the nitty-gritty of CSS, I thought it would be helpful to take a little trip down memory lane and understand _why_ CSS came to be in the first place. It wasn't always around, and its arrival was a pretty big deal for the web! 

## The "Academic" Web and the Need for Style <a id="the-academic-web"></a>

Back in the early days of the internet, websites were… well, let's just say they weren't winning any design awards. Most pages looked very similar, with simple text and basic formatting. Think of it like reading a research paper – informative, but not exactly visually exciting.

People quickly realized that they wanted more control over how their web pages looked. They wanted to add colors, change fonts, and generally make their websites more personal and engaging.

## The Inline Styling Era (and Why It Didn't Last) <a id="inline-styling"></a>

The first attempts at styling involved adding style information directly within the HTML code itself. HTML 3.2 introduced attributes like `color` and presentational tags like `<center>` and `<font>`.

Imagine trying to style every single piece of text on your website individually using these attributes! It quickly became a chaotic mess.

```html
<p><font color="red">This text is red.</font></p>
<h1 align="center"><font face="Arial" size="+2">My Centered Title</font></h1>
```

As you can see, this approach made the HTML code very cluttered and difficult to read. Plus, if you wanted to change the color of all your paragraphs, you'd have to go through every single `<p>` tag and change it manually! This was far from ideal and definitely not scalable.

## The Birth of CSS: Separating Structure from Style <a id="birth-of-css"></a>

This growing pain led to the development of **CSS**. The brilliant idea behind CSS was to move _all_ the presentation-related information out of the HTML and into separate files (or sections). This meant that HTML could go back to doing what it does best: defining the **structure** and **content** of the document. CSS would then handle how that content looked in the browser.

Think of it like this:

- **Before CSS:** HTML was responsible for both the content (what the words are) and the presentation (how they look). It was like writing a book where you also had to manually draw every font and decide the layout on each page.
- **With CSS:** HTML focuses on the content and structure (the chapters, headings, paragraphs), while CSS takes care of the presentation (the font styles, colors, layout). This makes the HTML cleaner and the styling much more organized and easier to manage.

## CSS is Always Evolving <a id="css-evolving"></a>

It's important to remember that CSS isn't a static thing. It's constantly evolving! The CSS you might have learned even just five years ago might have some outdated techniques, as new and better ways of styling emerge, and browsers get updated with new capabilities. It's a dynamic landscape, which keeps things exciting!

## A Look Back at the Browser Wars <a id="browser-wars"></a>

It's hard to imagine now, but when CSS was born, the web was a very different place. We had several competing web browsers, with **Internet Explorer** and **Netscape Navigator** being the main players.

Back then, styling was primarily done using HTML with those special presentational tags and attributes we talked about. This meant limited customization options, and a lot of the visual decisions were left up to the browser itself.

Even worse, different browsers often introduced their own _non-standard_ HTML tags to provide more styling power. This led to a frustrating situation where you often had to build your website specifically for one browser, and it might look completely different (or even broken) in another!

## The Realization: We Need a Standard! <a id="need-for-standard"></a>

People quickly realized the need for a standardized way to style web pages that would work consistently across all browsers. This is where the idea of CSS really took hold.

## The Birth of CSS Levels <a id="css-levels"></a>

After the initial idea was proposed in 1994, the first official version of CSS, **CSS Level 1 (CSS 1)**, was released in **1996**. This was a huge step forward in providing a standardized way to style web pages.

Then, in **1998**, **CSS Level 2 (CSS 2)** was published, adding even more powerful styling capabilities.

Since then, the way CSS is developed has changed. Instead of releasing big "levels," the **CSS Working Group** decided to break down new features into smaller, independent **modules**. This allows for more focused development and faster implementation of specific features by browsers.

## Browser Implementation: A Bit of a Rocky Start <a id="browser-implementation"></a>

Initially, browsers weren't exactly lightning-fast at fully supporting CSS. It took until around **2002** for the first browser to implement the full CSS specification: **Internet Explorer for Mac** (as nicely described in [this CSS Tricks post](https://css-tricks.com/look-back-history-css/)).

One particularly painful issue was that **Internet Explorer** (the dominant browser for many years) implemented the **box model** incorrectly right from the start. The box model is a fundamental concept in CSS layout (we'll learn about it later!), and this incorrect implementation led to years of headaches for web developers trying to make their websites look consistent across different browsers. We had to resort to various clever tricks and "hacks" to work around these browser inconsistencies.

## Where We Are Today: A Much Brighter Styling Landscape <a id="css-today"></a>

Thankfully, things are _much_, _much_ better today! For the most part, we can now use CSS standards without constantly worrying about browser quirks. Browsers have become much better at implementing CSS correctly and consistently.

We don't really have official "CSS Level" numbers anymore in the traditional sense. Instead, the CSS Working Group regularly releases "snapshots" of the CSS modules that are considered stable and ready for browsers to implement. The latest comprehensive snapshot was from **2018** ([https://www.w3.org/TR/css-2018/](https://www.w3.org/TR/css-2018/)).

**CSS Level 2** still forms the foundation of the CSS we write today, and all the newer features are built on top of it. CSS has never been more powerful, giving us incredible control over the look and feel of our websites.

## Key Takeaway <a id="key-takeaway"></a>

The history of CSS is a story of moving from a basic, unstructured way of styling to a more organized, standardized, and powerful system. Understanding this history helps us appreciate the benefits of using CSS and how far web development has come!

In the next lesson, we'll finally get our hands dirty and learn about the different ways you can actually _apply_ CSS to your HTML. Get excited!

</div>