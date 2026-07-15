# Exercise Solution: The Box Model, Sizing, Overflow, and Spacing

```html
<style>
  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }

  .card {
    width: 100%;
    max-width: 32rem;
    margin-inline: auto;
    padding: 1.25rem;
    border: 0.125rem solid #4b6f44;
    border-radius: 0.5rem;
    overflow-wrap: anywhere;
  }
</style>

<article class="card">
  <h1>Seed exchange</h1>
  <p>Bring labeled seeds and take varieties shared by neighbors.</p>
</article>
```

## Why this works

The card can shrink, stays capped at a readable width, includes padding in its width, and wraps unusually long text. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

