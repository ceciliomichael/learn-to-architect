# Exercise Solution: Two-Dimensional Layouts with Grid

```html
<style>
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 15rem), 1fr));
    gap: 1rem;
    padding: 0;
    list-style: none;
  }

  .gallery > li {
    padding: 1rem;
    background: #e8f0e5;
    color: #183018;
  }
</style>

<ul class="gallery">
  <li>Herbs</li>
  <li>Vegetables</li>
  <li>Flowers</li>
  <li>Fruit trees</li>
</ul>
```

## Why this works

The grid creates as many usable columns as fit and collapses to one column without a special breakpoint. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

