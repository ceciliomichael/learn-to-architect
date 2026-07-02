# Question 02: Optional vs Explicit Undefined

Look at these two interface definitions
```typescript
interface ShapeA {
  description?: string;
}

interface ShapeB {
  description: string | undefined;
}
```

1. Can you create `const a: ShapeA = {}` (omitting `description` entirely)? Why or why not?
2. Can you create `const b: ShapeB = {}` (omitting `description` entirely)? Why or why not?
3. What is the key practical difference between `property?: string` and `property: string | undefined`?

## ANSWER HERE

> **ShapeA  -  can you omit the property?**

> **ShapeB  -  can you omit the property?**

> **The key difference:**
