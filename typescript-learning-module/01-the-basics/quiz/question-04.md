# Question 04: any vs unknown

What is the practical difference between using `any` and `unknown` for a variable whose type you do not know yet?

Consider this code
```typescript
let valueA: any = "hello";
valueA.explode(); // What does TypeScript say?

let valueB: unknown = "hello";
valueB.explode(); // What does TypeScript say?
```

1. For each variable, what does TypeScript do when you call `.explode()` on it?
2. Which type should you always prefer and why?
3. What must you do before you can safely call `.toUpperCase()` on an `unknown` variable?

---

## ANSWER HERE

> **For `any` - calling .explode():**

> **For `unknown` - calling .explode():**

> **Which to prefer and why:**

> **What you must do before using unknown:**
