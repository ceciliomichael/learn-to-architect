# Challenge 02: Solution

```typescript
// utils/math.ts

export function add(a: number, b: number): number {
  return a + b;
}

export function multiply(a: number, b: number): number {
  return a * b;
}

export const TAX_RATE: number = 0.1;
```

---

```typescript
// index.ts

import { add, multiply, TAX_RATE } from "./utils/math";

const sum = add(5, 3);
console.log(sum); // 8

const product = multiply(4, 7);
console.log(product); // 28

const price = 100;
const total = price + price * TAX_RATE;
console.log("Total with tax: " + total); // "Total with tax: 110"
```
