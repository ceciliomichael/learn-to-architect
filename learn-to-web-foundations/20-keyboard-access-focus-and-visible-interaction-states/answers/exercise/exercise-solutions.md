# Exercise Solution: Keyboard Access, Focus, and Visible Interaction States

```html
<style>
  .skip-link {
    position: absolute;
    inset-inline-start: 1rem;
    inset-block-start: -5rem;
  }

  .skip-link:focus {
    inset-block-start: 1rem;
    padding: 0.75rem;
    background: Canvas;
    color: CanvasText;
    z-index: 10;
  }

  :focus-visible {
    outline: 0.2rem solid #d97706;
    outline-offset: 0.2rem;
  }
</style>

<a class="skip-link" href="#main-content">Skip to main content</a>
<nav aria-label="Primary"><a href="/events.html">Events</a></nav>
<main id="main-content" tabindex="-1">
  <h1>Garden events</h1>
  <button type="button">Show event details</button>
</main>
```

## Why this works

Focus follows source order, is always visible, the link navigates, and the button activates with native keyboard behavior. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

