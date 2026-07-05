# Question 01: unknown in catch

In TypeScript strict mode (specifically with `useUnknownInCatch` enabled by default in modern TypeScript), the `catch` variable is strictly typed as `unknown` rather than `any` or `Error`. Why does the compiler enforce this restriction?

```typescript
try {
  JSON.parse("not valid json");
} catch (error) {
  // In strict mode, 'error' is inferred as 'unknown'
  console.log(error.message); // Compiler Error: Object is of type 'unknown'.
}
```

Please answer the following three architectural questions:

1. **Why is `error` typed as `unknown` and not `Error`?** What does the JavaScript specification permit developers or third-party libraries to throw at runtime?
2. **What must you do before you can safely access `error.message` or `error.stack`?** What TypeScript operator or type guard technique should you apply?
3. **Write the corrected, production-grade version of the `catch` block** that safely handles both `Error` instances and unexpected non-error thrown values (such as raw strings or numbers).

## ANSWER HERE

> **1. Why `error` is typed as `unknown` instead of `Error`:**

> **2. What you must do before accessing `.message`:**

```typescript
// 3. Corrected, production-grade catch block:
try {
  JSON.parse("not valid json");
} catch (error: unknown) {
  // Implement safe narrowing and fallback handling here
}
```
