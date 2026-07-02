# Option 09: Type-Safe HTTP Router & Middleware Pipeline (Mini-tRPC/Hono)

**Difficulty:** Advanced
**Primary Concepts:** Method chaining, generic context accumulation, URL pattern matching, middleware design

---

## Why This Matters

Modern backend frameworks like tRPC, Hono, and Fastify let developers chain middleware together while passing typed context (e.g., attaching `user` in auth middleware so route handlers see `req.user` as strictly typed).

In standard Node.js/Express, middleware context is untyped (`req: any`). You will build a **type-safe router engine** where each middleware step enriches the request context type for subsequent handlers
---

## The Type Safety Requirement

```typescript
const app = new Router<{}>()
  // Step 1: Add logging middleware
  .use(async (req, next) => {
    console.log(req.method, req.path);
    return next(req);
  })
  // Step 2: Auth middleware enriches context with `{ user: { id: string } }`
  .use(async (req, next) => {
    if (!req.headers["authorization"]) {
      throw new UnauthorizedError("Missing token");
    }
    return next({ ...req, user: { id: "user-123" } });
  })
  // Step 3: Route handler receives enriched context
  .get("/profile", async (req) => {
    // TypeScript MUST know req.user.id exists and is a string
    return { status: 200, body: `Hello ${req.user.id}` };
  });
```

---

## Core Requirements

Build a `Router<TContext>` class supporting
```typescript
use<TNewContext>(
  middleware: (req: Request<TContext>, next: (enrichedReq: Request<TContext & TNewContext>) => Promise<Response>) => Promise<Response>
): Router<TContext & TNewContext>
// Notice how calling .use() returns a new Router typed with the combined context
get(path: string, handler: (req: Request<TContext>) => Promise<Response> | Response): Router<TContext>
post(path: string, handler: (req: Request<TContext>) => Promise<Response> | Response): Router<TContext>

handleRequest(method: string, path: string, headers?: Record<string, string>, body?: unknown): Promise<Response>
// Executes middleware chain sequentially. Catches custom errors and returns formatted error responses.
```

---

## Dynamic URL Parameters

Implement dynamic route matching for paths like `/users/:userId/orders/:orderId`.
When a request comes in for `/users/99/orders/50`, `req.params` must be populated with `{ userId: "99", orderId: "50" }`.

---

## What Your Final index.ts Should Demonstrate

1. Build an API router with auth middleware and rate-limiting middleware.
2. Simulate a GET request to `/users/42` with valid headers  -  show success.
3. Simulate a POST request without authorization headers  -  show 401 Unauthorized response handled cleanly by the pipeline.
