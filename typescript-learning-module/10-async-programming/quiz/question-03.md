# Question 03: Sequential vs Parallel

What is the difference between running async operations sequentially versus in parallel?

Two operations: `fetchA()` takes 1 second. `fetchB()` takes 1 second.

```typescript
// Sequential:
const a = await fetchA();
const b = await fetchB();

// Parallel:
const [a, b] = await Promise.all([fetchA(), fetchB()]);
```

1. How long does the sequential version take in total? Explain why.
2. How long does the parallel version take in total? Explain why.
3. When should you NOT use `Promise.all` (i.e. when must the tasks run one after another)?

## ANSWER HERE

> **Sequential  -  total time and why:**

> **Parallel  -  total time and why:**

> **When NOT to use Promise.all:**
