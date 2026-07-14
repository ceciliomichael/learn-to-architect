# Exercise Solution: Conditional Rendering

```tsx
export function Result({ count }: { count: number }) {
  return count === 0 ? <p>No results.</p> : <p>{count} results</p>;
}
```

## Why this works

Conditional rendering chooses element output with ordinary JavaScript while preserving meaningful empty and inaccessible states. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.