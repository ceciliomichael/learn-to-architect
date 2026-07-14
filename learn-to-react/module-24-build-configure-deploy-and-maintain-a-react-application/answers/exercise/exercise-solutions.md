# Exercise Solution: Build, Configure, Deploy, and Maintain a React Application

```tsx
function parsePublicUrl(value: unknown): URL {
  if (typeof value !== "string") throw new Error("Missing public API URL");
  const url = new URL(value);
  if (url.protocol !== "https:") throw new Error("Public API URL must use HTTPS");
  return url;
}
export const apiBase = parsePublicUrl(import.meta.env.VITE_PUBLIC_API_BASE);
```

## Why this works

Build and test the exact production artifact, expose only public configuration, and verify asset paths and rollback behavior. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.