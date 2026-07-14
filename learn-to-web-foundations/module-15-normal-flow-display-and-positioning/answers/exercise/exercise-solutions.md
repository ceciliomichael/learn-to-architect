# Exercise Solution: Normal Flow, Display, and Positioning

```html
<style>
  .notice {
    position: relative;
    padding: 1rem 1rem 1rem 3rem;
    border: 0.1rem solid #5e7758;
  }

  .notice__mark {
    position: absolute;
    inset-block-start: 1rem;
    inset-inline-start: 1rem;
  }
</style>

<aside class="notice" aria-labelledby="notice-title">
  <span class="notice__mark" aria-hidden="true">i</span>
  <h2 id="notice-title">Weather notice</h2>
  <p>The outdoor session moves inside when heavy rain begins.</p>
</aside>
```

## Why this works

The aside remains in normal flow while only its decorative mark is positioned relative to it. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

