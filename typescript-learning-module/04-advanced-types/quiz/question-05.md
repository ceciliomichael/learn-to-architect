# Question 05: Union vs. Intersection  -  Real-World Analogy

## Question

TypeScript has two ways to combine types
```typescript
type UnionExample        = TypeA | TypeB;   // A OR B
type IntersectionExample = TypeA & TypeB;   // A AND B
```

**Part 1:** In one sentence, describe what a **union type** guarantees about a value, and give a real-world analogy (not a code example).

**Part 2:** In one sentence, describe what an **intersection type** guarantees about a value, and give a real-world analogy (not a code example).

**Part 3:** Given the types below, list which properties are safe to access on `u` without narrowing, and which are safe to access on `i` without narrowing. Explain why.

```typescript
type WithEngine = { horsepower: number; startEngine(): void };
type WithSails  = { sailArea: number;   hoist(): void };

declare const u: WithEngine | WithSails;
declare const i: WithEngine & WithSails;
```

---

## Your Answer

```
// ANSWER HERE
```
