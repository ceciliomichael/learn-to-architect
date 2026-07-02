# Question 03: Structural Typing

TypeScript uses structural typing (shape-based compatibility). Consider this code:
```typescript
interface Point2D {
  x: number;
  y: number;
}

const point3D = {
  x: 10,
  y: 20,
  z: 30
};

const point: Point2D = point3D;
```

1. Does `const point: Point2D = point3D;` produce a TypeScript compiler error? Why or why not?
2. The object `point3D` has an extra property (`z`) that is not defined in `Point2D`. Why does TypeScript allow assigning it to a `Point2D` variable?
3. What would happen if `point3D` was missing the `y` property?

## ANSWER HERE

> **Does assigning point3D to point produce an error?**

> **Why TypeScript allows extra properties:**

> **What happens if property y is missing:**
