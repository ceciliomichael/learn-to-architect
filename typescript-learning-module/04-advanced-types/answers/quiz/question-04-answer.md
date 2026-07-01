# Question 04 Answer

**What TypeScript sees when `triangle` is added but not handled:**

When `triangle` is added to the union, `Shape` becomes:
```typescript
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number }
  | { kind: "triangle"; base: number; height: number };
```

In the switch statement, `"circle"` and `"square"` are handled. When a `Shape` with `kind: "triangle"` reaches the `default` case, TypeScript sees that `state` at that point has type `{ kind: "triangle"; base: number; height: number }`  -  because the two handled cases have been ruled out.

The line `const check: never = state` then tries to assign this remaining triangle type to a variable typed as `never`. Since `{ kind: "triangle"; ... }` is not assignable to `never`, TypeScript produces an error.

**The exact error produced:**
```
Type '{ kind: "triangle"; base: number; height: number; }' is not assignable to type 'never'.
```

**Why this protects the codebase:**
Without this check, adding a new shape to the union would compile silently. The `area` function would return `undefined` for triangles at runtime (since no case matched), which is a silent, hard-to-find bug. The `never` check converts a potential runtime bug into an immediate compile-time error, forcing the developer to handle every possible state.
