# Exercise Solution: Loading UI, Streaming, and Suspense

```tsx
export default function Loading() {
  return <p role="status">Loading account details...</p>;
}
```

## Why this works

A loading file and Suspense boundaries let ready parts render while slower server work continues, but each fallback must be meaningful and accessible. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.