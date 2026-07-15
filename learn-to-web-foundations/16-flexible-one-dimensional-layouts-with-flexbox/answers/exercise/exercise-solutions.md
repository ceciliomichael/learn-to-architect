# Exercise Solution: Flexible One-Dimensional Layouts with Flexbox

```html
<style>
  .card-list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    padding: 0;
    list-style: none;
  }

  .card-list > li {
    flex: 1 1 16rem;
    min-width: 0;
    padding: 1rem;
    border: 0.1rem solid #667a61;
  }
</style>

<ul class="card-list">
  <li><h2>Composting</h2><p>Learn the basics.</p></li>
  <li><h2>Seed saving</h2><p>Store seeds safely.</p></li>
  <li><h2>Watering</h2><p>Use water carefully.</p></li>
</ul>
```

## Why this works

Cards share wide rows, wrap before becoming too narrow, and retain logical source order. Treat this as a reference implementation, then compare it with every exercise step in developer tools. Different content and class names are valid when they preserve the same semantic, responsive, and accessibility contracts.

