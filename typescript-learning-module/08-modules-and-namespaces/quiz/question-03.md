# Question 03: Type-Only Imports (`import type`) and Build Bundle Optimization

In full-stack TypeScript applications and modular frontend architectures, distinguishing between runtime dependencies and compile-time type blueprints is critical for optimizing build performance and preventing bundle bloat.

Consider the following scenario: You are building a frontend React component that renders a table of user accounts. The component imports domain models from a shared library:

```typescript
// ============================================================================
// FILE: src/components/UserTable.ts (Frontend Client Component)
// ============================================================================
// Standard runtime import:
import { UserProfile, UserRole, UserDatabaseDriver } from "../models/userDomain";

export function renderUserRow(user: UserProfile, role: UserRole): string {
  return `<tr><td>${user.name}</td><td>${role}</td></tr>`;
}
```

In `src/models/userDomain.ts`, `UserProfile` and `UserRole` are TypeScript interfaces and type aliases, while `UserDatabaseDriver` is a heavy runtime class that imports Node.js database connectors and filesystem drivers.

## Your Challenge

Answer the following four architectural questions directly inside the **ANSWER HERE** block below. Do not use em dashes anywhere in your response!

1. In the code above, even though `renderUserRow` never instantiates or calls `UserDatabaseDriver` at runtime, why might a standard `import` statement cause a web build bundler (like Vite or Webpack) to include `UserDatabaseDriver` and all its Node.js database connectors inside the client browser JavaScript bundle?
2. How do you rewrite the import statement using **`import type`** to guarantee that `UserProfile` and `UserRole` are treated strictly as compile-time blueprints? What happens to `import type` statements during the JavaScript emission phase of the TypeScript compiler (`tsc`)?
3. What is the modern TypeScript (v4.5+) syntax for mixing standard runtime imports and type-only imports inside a single import statement? Show an example importing runtime class `UserDatabaseDriver` alongside type blueprints `UserProfile` and `UserRole`.
4. How does using `import type` improve incremental build speeds and hot-module replacement (HMR) performance in large enterprise monorepos?

---

## ANSWER HERE

### 1. Why standard imports risk client bundle bloat:
> 

### 2. Rewriting with `import type` and compilation behavior:
```typescript
// Write your type-only import statement here:
```
> **What happens during JS emission:**
> 

### 3. Modern inline type import syntax (TypeScript v4.5+):
```typescript
// Write your inline mixed import statement here:
```

### 4. Impact on incremental build speeds and HMR performance:
> 
