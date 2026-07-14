# Exercise Solution: Responsive Design, Media Queries, and Container Queries

```html
<style>
  .event-region {
    container-type: inline-size;
  }

  .event {
    display: grid;
    gap: 0.75rem;
    padding: 1rem;
    border: 0.1rem solid #5c7355;
  }

  @container (min-width: 34rem) {
    .event {
      grid-template-columns: 2fr 1fr;
      align-items: start;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    * {
      scroll-behavior: auto;
    }
  }
</style>

<div class="event-region">
  <article class="event">
    <div><h2>Seed swap</h2><p>Bring labeled seeds.</p></div>
    <p><time datetime="2026-09-12">September 12</time></p>
  </article>
</div>
```

## Why this works

The component works as one column and gains a second column only when its own space allows. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

