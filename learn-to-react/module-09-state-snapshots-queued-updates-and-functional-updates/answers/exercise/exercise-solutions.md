# Exercise Solution: State Snapshots, Queued Updates, and Functional Updates

```tsx
import type { Dispatch, SetStateAction } from "react";
export function incrementTwice(setCount: Dispatch<SetStateAction<number>>) {
  setCount(previous => previous + 1);
  setCount(previous => previous + 1);
}
```

## Why this works

Each render sees a state snapshot; use functional updates when the next value depends on the queued previous value. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.