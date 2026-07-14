# Exercise Solution: Route Handlers and HTTP Contracts

```tsx
export async function POST(request: Request) {
  const session = await requireApiSession(request);
  const input = parseCreateItem(await request.json());
  const item = await createItem(session.userId, input);
  return Response.json(item, { status: 201 });
}
```

## Why this works

A route handler implements an HTTP contract with Web Request and Response APIs. Parse input, validate it, enforce access, choose status codes, and return a stable response shape. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.