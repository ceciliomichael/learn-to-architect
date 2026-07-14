# Exercise Solution: Rendering, Network, and Asset Performance

```ts
const started = performance.now();
requestAnimationFrame(() => {
  requestAnimationFrame(() => {
    console.log(`Two paint opportunities: ${performance.now() - started}ms`);
  });
});
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

