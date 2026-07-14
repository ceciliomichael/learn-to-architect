# Exercise Solution: Transforms, Transitions, Animation, and Reduced Motion

```html
<style>
  .details {
    transition: transform 180ms ease, opacity 180ms ease;
  }

  .details[hidden] {
    display: block;
    opacity: 0;
    transform: translateY(-0.5rem);
    visibility: hidden;
  }

  @media (prefers-reduced-motion: reduce) {
    .details {
      transition: none;
      transform: none;
    }
  }
</style>

<button type="button" aria-expanded="true" aria-controls="details">
  Workshop details
</button>
<div class="details" id="details">
  <p>Meet beside the greenhouse at 10:00 AM.</p>
</div>
```

## Why this works

The visual transition has a no-motion alternative and the content relationship is represented in HTML. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

