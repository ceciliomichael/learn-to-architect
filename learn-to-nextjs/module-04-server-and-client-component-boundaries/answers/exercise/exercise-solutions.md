# Exercise Solution: Server and Client Component Boundaries

```tsx
// app/counter.tsx
"use client";
import { useState } from "react";
export function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(value => value + 1)}>Count: {count}</button>;
}
```

## Why this works

Components in the App Router are Server Components unless a client boundary is declared. Add use client only where browser state, effects, event handlers, or browser APIs are required. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.