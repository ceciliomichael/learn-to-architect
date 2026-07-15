# Exercise Solution: Async Data, Cancellation, Loading, Empty, and Error States

```tsx
type LoadState<T> = { status: "loading" } | { status: "error"; message: string } | { status: "ready"; data: T };
```

## Why this works

Async UI needs owned cancellation plus distinct loading, empty, error, and success states, and stale results must not overwrite newer intent. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.