# Exercise Solution: Accessibility, Security Headers, and Untrusted Content

```tsx
export function SafeComment({ text }: { text: string }) {
  return <p className="comment">{text}</p>;
}
```

## Why this works

Preserve semantic HTML and keyboard behavior, apply security headers deliberately, validate untrusted content, and avoid rendering raw HTML unless it has a proven sanitization boundary. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.