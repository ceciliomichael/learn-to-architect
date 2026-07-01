# Question 01: unknown in catch

In TypeScript strict mode, the `catch` variable is typed as `unknown`. Why?

```typescript
try {
  JSON.parse("not valid json");
} catch (error) {
  // error is 'unknown'
  console.log(error.message); // TypeScript error!
}
```

1. Why is `error` typed as `unknown` and not `Error`?
2. What must you do before you can safely access `error.message`?
3. Write the corrected version of the `catch` block.

## ANSWER HERE

> **Why `error` is `unknown`:**

> **What you must do before accessing `.message`:**

```typescript
// Corrected catch block:
catch (error) {

}
```
