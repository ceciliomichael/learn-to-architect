# Question 03: Type Predicates

What is the difference between these two function signatures?

```typescript
// Version A:
function isCat(pet: Cat | Dog): boolean { ... }

// Version B:
function isCat(pet: Cat | Dog): pet is Cat { ... }
```

1. If you use Version A inside an `if (isCat(pet))` block, what type does TypeScript think `pet` is inside that block?
2. If you use Version B inside an `if (isCat(pet))` block, what type does TypeScript think `pet` is inside that block?
3. What extra information does `pet is Cat` give the TypeScript compiler that a plain `boolean` return type does not?

## ANSWER HERE

> **Inside if-block with Version A:**

> **Inside if-block with Version B:**

> **What `pet is Cat` tells the compiler:**
