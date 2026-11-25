---
title: "Why I'm Learning Astro"
description: "A few things I noticed while building a simple blog with Astro."
category: "Astro"
pubDate: 2026-11-24
cover: "../../assets/astro.jpg"
coverAlt: "Astro graphic with the words Build the web you want"
---

Astro is a web framework for building content-focused sites, such as blogs, documentation, and portfolios. It turns pages and components into HTML that visitors can read in their browsers. By default, Astro does not send JavaScript for every component, which is useful when a site is mostly text and images.

I can write an Astro component using familiar HTML and add JavaScript in its frontmatter when I need to prepare data. If a part of the site needs interactivity later, Astro can include a client-side component just for that part.

## How pages work

Astro uses file-based routing: a file in `src/pages` becomes a URL. For example, `src/pages/about.astro` creates an `/about` page. An Astro page can contain both JavaScript and markup:

```astro
---
const heading = "About this blog";
---

<main>
  <h1>{heading}</h1>
  <p>Notes from learning web development.</p>
</main>
```

The code between the `---` lines runs to prepare the page. The markup below it describes what gets rendered. Layouts let multiple pages share the same outer structure, such as a header and footer.

## Pages and content

Writing a separate page component for every blog post would repeat a lot of markup. Astro's content collections let me keep posts as Markdown files with a common set of details, such as a title, date, and cover image. A schema checks that each post has the information the page needs.

The collection can be queried from an Astro component to build a list of links:

```astro
---
import { getCollection } from "astro:content";

const posts = await getCollection("blog");
---

<ul>
  {posts.map((post) => (
    <li><a href={`/blog/${post.id}/`}>{post.data.title}</a></li>
  ))}
</ul>
```

A dynamic route can also make one article page for each Markdown file. That way, I can change the article layout in one place instead of editing every post.

## Why I chose it

I chose Astro for this blog because the main job of the site is to display articles. I wanted to practice building pages and components while keeping the writing in simple Markdown files. Astro gives me a way to organize those posts without adding a lot of client-side code to a site that does not need it yet.

I am still learning, so I like being able to start with a few working pages and add features gradually. Later I might try tags or search, but for now I can focus on writing, making the posts easy to read, and understanding how the pieces fit together.
