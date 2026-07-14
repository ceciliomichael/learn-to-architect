# Exercise Solution: Components, Imports, Exports, and Purity

```tsx
export default function Status() {
  return <p>Registration is open.</p>;
}
```

## Why this works

A component is a capitalized function that returns UI and remains pure during rendering; imports and exports define module ownership. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.