# Question 01: Union vs Intersection

Given
```typescript
type A = { name: string };
type B = { age: number };
type UnionAB        = A | B;
type IntersectionAB = A & B;
```

1. You have `val: UnionAB`. Can you safely write `val.name` without a check? Why?
2. You have `val2: IntersectionAB`. Can you safely write `val2.name` without a check? Why?
3. In one sentence each, give a real-world analogy for union and intersection.

## ANSWER HERE

> **Union  -  can you access `val.name` directly?**

> **Intersection  -  can you access `val2.name` directly?**

> **Real-world analogy for union:**

> **Real-world analogy for intersection:**
