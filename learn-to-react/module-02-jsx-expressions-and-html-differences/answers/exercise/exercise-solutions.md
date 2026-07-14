# Exercise Solution: JSX, Expressions, and HTML Differences

```tsx
export function Greeting() {
  const name = "Ada";
  return <h1 className="greeting">Hello, {name}</h1>;
}
```

## Why this works

JSX describes a React element tree while JavaScript expressions supply values; use className, htmlFor, and camel-cased properties where React differs from HTML source. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.