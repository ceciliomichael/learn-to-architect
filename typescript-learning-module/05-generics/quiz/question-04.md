# Question 04

## Question

- What is a **tuple type** in TypeScript?
- How is `[string, number]` different from `(string | number)[]`?
- Give a concrete scenario where you would use a tuple instead of a union array.

Consider these two variables
```typescript
let a: [string, number] = ["Alice", 30];
let b: (string | number)[] = ["Alice", 30];
```

What can TypeScript tell you about `a[0]` that it cannot tell you about `b[0]`?

---

## ANSWER HERE

> Write your answer below. Cover positional typing, fixed length, and give a real-world use case (e.g., a function return value).
