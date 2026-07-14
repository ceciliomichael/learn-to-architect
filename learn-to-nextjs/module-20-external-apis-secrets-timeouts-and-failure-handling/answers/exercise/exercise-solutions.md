# Exercise Solution: External APIs, Secrets, Timeouts, and Failure Handling

```tsx
const controller = new AbortController();
const timer = setTimeout(() => controller.abort(), 5000);
try {
  const response = await fetch(apiUrl, { signal: controller.signal, headers: { Authorization: `Bearer ${apiToken}` } });
  if (!response.ok) throw new Error(`Upstream failed: ${response.status}`);
  return parseUpstream(await response.json());
} finally {
  clearTimeout(timer);
}
```

## Why this works

Call external APIs only from the environment that may hold their secrets, set a timeout or cancellation policy, validate responses, and translate failures into useful application states. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.