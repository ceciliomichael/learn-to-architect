# Exercise Solution: Lists, Stable Keys, and Empty States

```tsx
const items = [{ id: "water", label: "Water" }];
export function Tasks() {
  return <ul>{items.map(item => <li key={item.id}>{item.label}</li>)}</ul>;
}
```

## Why this works

Render arrays with stable keys derived from data identity and provide an intentional empty state. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.