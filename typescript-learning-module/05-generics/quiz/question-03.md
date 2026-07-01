# Question 03: Tuples

What is a tuple type in TypeScript?

```typescript
type Coordinate = [number, number];
type NameAndAge  = [string, number];

const point: Coordinate = [10, 20];
const entry: NameAndAge  = ["Alice", 30];
```

1. How is the tuple type `[string, number]` different from the union array type `(string | number)[]`?
2. What TypeScript error do you get if you write `const bad: NameAndAge = [30, "Alice"]` (wrong order)?
3. Give a real-world scenario where a tuple is more appropriate than an interface.

## ANSWER HERE

> **Difference between `[string, number]` and `(string | number)[]`:**

> **Error when order is wrong:**

> **Real-world scenario for a tuple:**
