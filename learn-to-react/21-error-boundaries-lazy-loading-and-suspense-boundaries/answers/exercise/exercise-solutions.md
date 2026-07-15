# Exercise Solution: Error Boundaries, Lazy Loading, and Suspense Boundaries

```tsx
import { lazy, Suspense } from "react";
const Settings = lazy(() => import("./Settings"));
export function SettingsPage() {
  return <Suspense fallback={<p role="status">Loading settings...</p>}><Settings /></Suspense>;
}
```

## Why this works

Error boundaries contain rendering failures, lazy loading splits code, and Suspense boundaries represent supported waiting work. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.