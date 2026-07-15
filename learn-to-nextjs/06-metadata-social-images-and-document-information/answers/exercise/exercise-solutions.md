# Exercise Solution: Metadata, Social Images, and Document Information

```tsx
import type { Metadata } from "next";
export const metadata: Metadata = {
  title: "About | Example",
  description: "Learn about the Example team."
};
```

## Why this works

Metadata describes pages to browsers and sharing services. Use a static metadata export for fixed values and generateMetadata for values that depend on route data. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.