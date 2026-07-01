# Question 02: Missing await

You write this code (note: NO `await`):

```typescript
async function fetchUserData(): Promise<{ name: string }> {
  return new Promise((resolve) => setTimeout(() => resolve({ name: "Alice" }), 500));
}

async function main() {
  const data = fetchUserData(); // No await!
  console.log(data.name);      // What happens here?
}
```

1. What is the type of `data`? What would you see if you `console.log(data)` immediately?
2. What TypeScript error (if any) does `data.name` produce?
3. What is the one-word fix?

## ANSWER HERE

> **Type of `data` and what `console.log(data)` shows:**

> **Error on `data.name`:**

> **The fix:**
