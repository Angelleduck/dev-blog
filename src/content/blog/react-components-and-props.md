---
title: "React Components and Props"
description: "A beginner-friendly way to think about reusable React components."
category: "Frontend"
pubDate: 2026-11-22
cover: "../../assets/reactjs.png"
coverAlt: "React logo above the words React JS"
---

React is a JavaScript library for building user interfaces. A React component is usually a function that returns JSX: markup-like code describing what should appear on the screen. A page can be made from many small components, such as a header, a list, and a card for each item.

Components are useful when the same kind of content appears more than once. Instead of copying a card's markup three times, one component can display three different sets of data.

## Passing data with props

Props are values passed **from a parent component to a child component**. A `PostCard` might receive a title and a description. The card decides how those values are displayed, but the parent decides what each card says.

```jsx
function PostCard({ title, description }) {
  return (
    <article>
      <h2>{title}</h2>
      <p>{description}</p>
    </article>
  );
}

function PostList() {
  return (
    <section>
      <PostCard
        title="Learning React"
        description="Starting with components and props."
      />
      <PostCard
        title="Learning Astro"
        description="Building pages for a small blog."
      />
    </section>
  );
}
```

`PostList` is the parent in this example. It uses `PostCard` twice with different props, so the structure stays the same while the content changes. The `{title}` and `{description}` expressions put those values into the JSX.

## Rendering a list

When the posts come from an array, the parent can use `map()` instead of writing each card by hand:

```jsx
const posts = [
  { id: 1, title: "Learning React", description: "Components and props." },
  { id: 2, title: "Learning Astro", description: "Pages and content." },
];

function PostList() {
  return (
    <section>
      {posts.map((post) => (
        <PostCard
          key={post.id}
          title={post.title}
          description={post.description}
        />
      ))}
    </section>
  );
}
```

The `key` helps React identify each card when the list changes. A stable ID is a better key than the item's position in the array.

## Props are not state

Props are read-only from the receiving component's point of view. `PostCard` should display the title it receives, not try to change that prop directly. If a value needs to change after a user clicks a button, the component that owns the value can use state and pass the updated value down as a prop.

For practice, try adding a third post to the array or giving `PostCard` a new `category` prop. One small change to the card can then update every item in the list.
