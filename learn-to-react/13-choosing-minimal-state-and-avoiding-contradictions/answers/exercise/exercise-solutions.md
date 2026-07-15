# Exercise Solution: Choosing Minimal State and Avoiding Contradictions

```tsx
type Item = { id: string; label: string };
export function filterItems(items: Item[], query: string): Item[] {
  const normalized = query.trim().toLowerCase();
  return items.filter(item => item.label.toLowerCase().includes(normalized));
}
```

## Why this works

Store the minimum complete state and derive everything else during rendering when possible. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.