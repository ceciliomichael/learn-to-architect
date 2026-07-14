# Exercise Solution: Fetch, HTTP Results, Headers, and Content Types

```ts
type Product = { readonly name: string };

async function loadProduct(id: string): Promise<unknown> {
  const url = new URL(`/api/products/${encodeURIComponent(id)}`, location.origin);
  const response = await fetch(url, {
    headers: { Accept: "application/json" },
  });

  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }

  const type = response.headers.get("content-type") ?? "";
  if (!type.includes("application/json")) {
    throw new Error("Expected JSON response");
  }

  return response.json();
}
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

