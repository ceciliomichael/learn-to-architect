# Exercise Solution: Reducers for Related State Transitions

```tsx
type Action = { type: "increment" } | { type: "reset" };
function reducer(state: number, action: Action) {
  return action.type === "reset" ? 0 : state + 1;
}
```

## Why this works

A reducer names related state transitions and keeps each action deterministic. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.