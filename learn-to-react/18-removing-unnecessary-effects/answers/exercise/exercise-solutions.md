# Exercise Solution: Removing Unnecessary Effects

```tsx
export function formatFullName(firstName: string, lastName: string): string {
  return `${firstName} ${lastName}`;
}
```

## Why this works

Remove an effect when derived rendering, an event handler, a key, or an external-store API expresses the behavior directly. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.