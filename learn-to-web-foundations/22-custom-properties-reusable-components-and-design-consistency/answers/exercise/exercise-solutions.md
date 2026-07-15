# Exercise Solution: Custom Properties, Reusable Components, and Design Consistency

```html
<style>
  :root {
    --color-accent: #285f2a;
    --color-on-accent: #ffffff;
    --space-2: 0.5rem;
    --space-3: 1rem;
    --radius: 0.4rem;
  }

  .button {
    display: inline-block;
    padding: var(--space-2) var(--space-3);
    border: 0.125rem solid var(--color-accent);
    border-radius: var(--radius);
    background: var(--color-accent);
    color: var(--color-on-accent);
    font: inherit;
  }

  .button--quiet {
    background: transparent;
    color: var(--color-accent);
  }
</style>

<button class="button" type="button">Join workshop</button>
<button class="button button--quiet" type="button">Cancel</button>
```

## Why this works

Shared decisions come from named properties and one base class, while the quiet variant changes only its intended difference. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

