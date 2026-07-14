# Exercise Solution: Context and Reducer Composition

```tsx
import { createContext } from "react";
export const CountContext = createContext<number | null>(null);
```

## Why this works

Context supplies stable cross-tree dependencies and can pair with a reducer for shared transitions. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.