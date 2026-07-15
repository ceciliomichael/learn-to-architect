# Exercise Solution: Cache Behavior and Explicit Freshness

```tsx
import { cacheLife } from "next/cache";
async function loadCatalog() {
  "use cache";
  cacheLife("minutes");
  return readCatalog();
}
```

## Why this works

Treat freshness as an explicit product decision. Know whether data can be reused, for how long, and what event makes it stale, then use the current cache and revalidation APIs deliberately. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.