# Question 04: The never Exhaustiveness Check

A developer starts with this discriminated union and switch
```typescript
type Shape = { kind: "circle"; radius: number } | { kind: "square"; side: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle": return 3.14 * shape.radius ** 2;
    case "square": return shape.side * shape.side;
    default
      const check: never = shape;
      return check;
  }
}
```

Later, a teammate adds `| { kind: "triangle"; base: number; height: number }` to the `Shape` type but does not add a `case "triangle"` to the switch.

Walk through exactly what TypeScript sees and what error it produces. Why does this protect the codebase?

## ANSWER HERE

> **What TypeScript sees when triangle is added but not handled:**

> **The exact error produced:**

> **Why this protects the codebase:**
