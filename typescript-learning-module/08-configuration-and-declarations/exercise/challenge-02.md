# Challenge 02: Modules  -  Named and Default Exports

Practice splitting code across files using TypeScript module exports.

## Your Task

Write the content of **two files** separated by a `---` line in your answer.

**File 1: `utils/math.ts`**
- Export a named function `add(a: number, b: number): number`.
- Export a named function `multiply(a: number, b: number): number`.
- Export a named constant `TAX_RATE: number = 0.1`.

**File 2: `index.ts`**
- Import `add`, `multiply`, and `TAX_RATE` from `./utils/math`.
- Calculate `5 + 3` using `add` and log the result.
- Calculate `4 * 7` using `multiply` and log the result.
- Calculate a price of `100` plus tax (`100 * TAX_RATE`) and log `"Total with tax: " + result`.

## ANSWER HERE

```typescript
// utils/math.ts



---
// index.ts


```
