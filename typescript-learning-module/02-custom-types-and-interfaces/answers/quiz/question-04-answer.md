# Question 04 Answer

**What only `type` can do (with example):**
A `type` alias can represent primitives, union types, intersection types, tuples, and any other type expression  -  not just object shapes. An `interface` can only describe object shapes.

```typescript
// These are impossible with 'interface':
type StringOrNumber = string | number;
type Coordinates = [number, number];
type ID = string;
```

You cannot write `interface StringOrNumber = string | number`. That is a syntax error.

**What only `interface` can do:**
Declaration merging. If you declare the same `interface` name twice in the same scope, TypeScript automatically merges the two declarations into one. With `type`, declaring the same name twice is always a compiler error (`Duplicate identifier`).

This makes `interface` the preferred choice when writing library code or when you expect others to extend your types  -  they can add to an existing interface without modifying the original file.
