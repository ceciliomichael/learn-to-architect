# Exercise Solution: Server Data Fetching and Request Ownership

```tsx
type Product = { id: string; name: string };
async function loadProducts(): Promise<Product[]> {
  const response = await fetch("https://example.test/products");
  if (!response.ok) throw new Error("Products could not be loaded");
  return validateProducts(await response.json());
}
```

## Why this works

Fetch data in the server component or server function that owns its use, validate the response, and keep credentials on the server. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.