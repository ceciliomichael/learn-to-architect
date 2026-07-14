# Exercise Solution: Cookies, Headers, Redirects, and Request Context

```tsx
import { cookies } from "next/headers";
export async function readTheme() {
  const store = await cookies();
  return store.get("theme")?.value === "dark" ? "dark" : "light";
}
```

## Why this works

Cookies and headers belong to the current request context, redirects end the current response path, and reading request-specific values can affect rendering and caching behavior. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.