# Exercise Solution: Pages, Layouts, Links, and Navigation

```tsx
import Link from "next/link";
export default function RootLayout({ children }: Readonly<{ children: React.ReactNode }>) {
  return <html lang="en"><body><nav><Link href="/">Home</Link></nav>{children}</body></html>;
}
```

## Why this works

A page supplies a route, a layout wraps descendant routes, and Link performs accessible client navigation while retaining normal link behavior. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.