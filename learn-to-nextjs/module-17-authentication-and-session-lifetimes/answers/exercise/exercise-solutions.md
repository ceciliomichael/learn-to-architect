# Exercise Solution: Authentication and Session Lifetimes

```tsx
import { cookies } from "next/headers";
export async function requireSession() {
  const token = (await cookies()).get("session")?.value;
  const session = token ? await findValidSession(token) : null;
  if (session === null) throw new Error("Authentication required");
  return session;
}
```

## Why this works

Authentication proves which session is making a request, and session design must define creation, rotation, expiry, revocation, and secure cookie behavior. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.