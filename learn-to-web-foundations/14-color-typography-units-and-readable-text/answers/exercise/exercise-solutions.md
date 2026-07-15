# Exercise Solution: Color, Typography, Units, and Readable Text

```html
<style>
  :root {
    color-scheme: light dark;
    font-family: system-ui, sans-serif;
    line-height: 1.6;
  }

  body {
    margin: 0;
    padding: 1.5rem;
  }

  main {
    max-width: 65ch;
    margin-inline: auto;
  }

  .status {
    border-inline-start: 0.35rem solid currentColor;
    padding-inline-start: 0.75rem;
    font-weight: 700;
  }
</style>

<main>
  <h1>Workshop details</h1>
  <p class="status">Registration status: Open</p>
  <p>Bring gloves and a refillable water bottle.</p>
</main>
```

## Why this works

Text remains readable, lines stay constrained, and status has words plus a non-color border cue. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

