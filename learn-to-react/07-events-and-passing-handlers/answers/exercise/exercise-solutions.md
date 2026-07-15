# Exercise Solution: Events and Passing Handlers

```tsx
export function SaveButton({ onSave }: { onSave: () => void }) {
  return <button type="button" onClick={onSave}>Save</button>;
}
```

## Why this works

Pass event handlers as functions and keep the action owner explicit. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.