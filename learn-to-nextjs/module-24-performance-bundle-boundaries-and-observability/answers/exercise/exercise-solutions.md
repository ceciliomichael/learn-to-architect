# Exercise Solution: Performance, Bundle Boundaries, and Observability

```tsx
import dynamic from "next/dynamic";
const Chart = dynamic(() => import("./chart"));
export function Report() {
  return <section><h2>Monthly report</h2><Chart /></section>;
}
```

## Why this works

Measure server work, client bundle size, navigation, rendering, and failures before optimizing. Keep interactive client boundaries small and attach logs or traces to request context without recording secrets. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.