# Quiz Question 05

## Question

Consider this function overload
```typescript
// Overload signatures
function parseInput(value: string): string[];
function parseInput(value: number): string;

// Implementation signature
function parseInput(value: string | number): string[] | string {
  if (typeof value === 'string') {
    return value.split(',');
  } else {
    return value.toFixed(2);
  }
}
```

TypeScript **only exposes the overload signatures** to callers  -  the implementation signature is hidden.

1. Why does TypeScript restrict callers to the overload signatures instead of the implementation signature?
2. What **problem** does hiding the implementation signature solve?
3. If a caller tries `parseInput(true)` (passing a boolean), will TypeScript allow it? Why or why not?

---

## Why this matters

Function overloads are a powerful tool for expressing precise input/output relationships. Understanding *why* the implementation signature is hidden prevents common mistakes when defining and consuming overloaded functions. This is covered in **Section 9** of the README.

---

## Your Answer

```
ANSWER HERE
```
