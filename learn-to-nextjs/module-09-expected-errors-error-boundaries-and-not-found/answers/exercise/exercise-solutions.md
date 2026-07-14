# Exercise Solution: Expected Errors, Error Boundaries, and Not Found

```tsx
import { notFound } from "next/navigation";
export default async function PostPage({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  const post = await findPost(id);
  if (post === null) notFound();
  return <article><h1>{post.title}</h1></article>;
}
```

## Why this works

Return expected failures as ordinary states, use notFound for missing resources, and use an error boundary for unexpected rendering failures that need containment and recovery. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.