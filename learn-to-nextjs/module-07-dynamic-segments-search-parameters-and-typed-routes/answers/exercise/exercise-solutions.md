# Exercise Solution: Dynamic Segments, Search Parameters, and Typed Routes

```tsx
type PageProps = { params: Promise<{ productId: string }> };
export default async function ProductPage({ params }: PageProps) {
  const { productId } = await params;
  if (!/^[a-z0-9-]+$/.test(productId)) return <p>Invalid product address.</p>;
  return <h1>Product {productId}</h1>;
}
```

## Why this works

Dynamic segment folders capture path values, search parameters represent query values, and both remain untrusted input even when TypeScript describes their shape. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.