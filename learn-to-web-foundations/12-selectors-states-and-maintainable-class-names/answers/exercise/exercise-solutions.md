# Exercise Solution: Selectors, States, and Maintainable Class Names

```html
<style>
  .action-link {
    color: #145da0;
    font-weight: 700;
    text-underline-offset: 0.2em;
  }

  .action-link:hover {
    text-decoration-thickness: 0.18em;
  }

  .action-link:focus-visible {
    outline: 0.2rem solid #f0a000;
    outline-offset: 0.2rem;
  }

  .action-link[aria-current="page"] {
    color: #173b17;
  }
</style>

<nav aria-label="Primary">
  <a class="action-link" href="/" aria-current="page">Home</a>
  <a class="action-link" href="/events.html">Events</a>
</nav>
```

## Why this works

One reusable class provides base styling while state selectors add visible, non-color-only cues. Use the browser inspector to connect each exercise requirement to the exact element, attribute, rule, request, or computed value that satisfies it. File names and content may differ when the same semantic and accessibility contracts are preserved.

