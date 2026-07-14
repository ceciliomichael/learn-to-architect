# Exercise Solution: Props, Children, and Composition

```tsx
type PanelProps = { title: string; children: React.ReactNode };
export function Panel({ title, children }: PanelProps) {
  return <section><h2>{title}</h2>{children}</section>;
}
```

## Why this works

Props are readonly inputs and children supports composition without making a component know every nested use. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.