# Exercise Solution: App Router Folders, Files, and Colocation

```tsx
export default function AccountPage() {
  return <main><h1>Account</h1></main>;
}
// app/account/format-name.ts is colocated code, not a route.
```

## Why this works

Inside app, folders organize route segments while special file names such as page, layout, loading, error, and route give files framework meaning. Ordinary colocated files are not public routes by themselves. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.