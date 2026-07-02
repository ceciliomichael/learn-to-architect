# Question 01: Type Erasure & Boundary Vulnerability

A junior developer presents the following code in a code review
```typescript
interface UserData {
  id: string;
  email: string;
  isAdmin: boolean;
}

async function handleLogin(reqBody: unknown): Promise<void> {
  const user = reqBody as UserData;
  if (user.isAdmin) {
    grantAdminAccess(user.id);
  }
}
```

1. Explain precisely why this code compiles with zero errors under `strict: true`.
2. Explain what happens at runtime if an attacker sends `{ id: "hacker-1" }` (omitting `isAdmin`) versus sending `{ id: "hacker-2", isAdmin: "true" }` (string `"true"` instead of boolean).
3. Why does the `as UserData` type assertion fail to protect the system?
4. Write the corrected, production-grade version of `handleLogin` using a runtime narrowing check or type predicate.

## ANSWER HERE

> **1. Why it compiles:**

> **2. Runtime impact of both payloads:**

> **3. Why `as` fails here:**

```typescript
// 4. Corrected implementation
```
