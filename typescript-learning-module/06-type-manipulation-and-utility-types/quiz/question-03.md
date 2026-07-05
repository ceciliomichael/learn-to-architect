# Question 03: typeof in the Type System

When `typeof` appears inside a type declaration, what does it do? Is it the same as the `typeof` you use in `if (typeof x === "string")`?

```typescript
const serverConfig = {
  host: "localhost",
  port: 3000,
  secure: false
};

type ServerConfig = typeof serverConfig;
```

1. Does `typeof serverConfig` execute at runtime when TypeScript compiles this? Explain.
2. What is the exact inferred type of `ServerConfig`?
3. Give one practical scenario where extracting a type with `typeof` is more useful than writing the interface manually.

## ANSWER HERE

> **Does it execute at runtime?**

> **Exact type of `ServerConfig`:**

> **Practical scenario:**
