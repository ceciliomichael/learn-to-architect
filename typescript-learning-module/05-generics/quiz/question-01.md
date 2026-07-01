# Question 01: any vs Generic

Why is a generic function safer than using `any`?

```typescript
function processAny(arg: any): any {
  return arg;
}

function processSafe<T>(arg: T): T {
  return arg;
}
```

1. You call `const result1 = processAny("hello")`. What does TypeScript think `result1` is? What would happen if you called `result1.toFixed(2)`?
2. You call `const result2 = processSafe("hello")`. What does TypeScript think `result2` is? What would happen if you called `result2.toFixed(2)`?
3. In one sentence, explain what a generic type variable (`<T>`) actually does.

## ANSWER HERE

> **Type of `result1` and what happens with `.toFixed(2)`:**

> **Type of `result2` and what happens with `.toFixed(2)`:**

> **What `<T>` does:**
