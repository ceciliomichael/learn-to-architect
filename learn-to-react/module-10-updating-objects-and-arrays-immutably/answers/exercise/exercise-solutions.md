# Exercise Solution: Updating Objects and Arrays Immutably

```tsx
type Item = { id: string; label: string };
export function addItem(items: Item[], label: string): Item[] {
  return [...items, { id: crypto.randomUUID(), label }];
}
```

## Why this works

Replace state objects and arrays without mutation so React and readers can observe a new value. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.