# Question 01: Object Shape Transformations and Memory Models

Analyze how TypeScript's built-in shape transformation utilities (`Partial<T>`, `Required<T>`, and `Readonly<T>`) manipulate interface rules at compile time.

```typescript
interface DatabaseUser {
  id: string;
  username?: string;
  email: string;
  createdAt: Date;
}
```

## Questions

1. **Structural Comparison**: What is the exact architectural difference between `Partial<DatabaseUser>` and manually defining an interface where every property is typed as `value | undefined` (e.g., `id: string | undefined;`)? Explain how optional properties behave when checking object keys using `Object.keys()` or `'key' in obj`.
2. **Required Modifier Mechanics**: When you apply `Required<DatabaseUser>`, what happens to the `username?: string` property? How does the compiler enforce this when validating new object literals?
3. **Runtime vs Compile-Time Enforcement**: If you declare a variable as `const user: Readonly<DatabaseUser>` and try to reassign `user.email = "new@test.com"`, TypeScript produces a compiler error. What happens if this code is forcefully transpiled and run in Node.js or a browser? Does `Readonly<T>` freeze the object in runtime memory like `Object.freeze()`? Explain why or why not.

## ANSWER HERE

> **1. Structural Comparison (`Partial` vs `| undefined`):**

> **2. Required Modifier Mechanics:**

> **3. Runtime vs Compile-Time Enforcement (`Readonly`):**
