# Exercise Solution: Rendering Performance, Profiling, and Measured Optimization

```tsx
import { useMemo } from "react";
type Item = { id: string; label: string };
export function useVisibleItems(items: Item[], query: string) {
  return useMemo(() => items.filter(item => item.label.includes(query)), [items, query]);
}
```

## Why this works

Profile first, keep state local, and optimize measured rendering work rather than adding memoization everywhere. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.