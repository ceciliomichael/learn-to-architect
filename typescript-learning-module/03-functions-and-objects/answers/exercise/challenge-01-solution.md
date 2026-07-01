# Challenge 01: Solution

```typescript
function calculate(
  operation: "ADD" | "SUBTRACT" | "MULTIPLY" | "DIVIDE",
  a: number,
  b: number
): number {
  if (operation === "DIVIDE" && b === 0) {
    throw new Error("Cannot divide by zero.");
  }

  if (operation === "ADD")      return a + b;
  if (operation === "SUBTRACT") return a - b;
  if (operation === "MULTIPLY") return a * b;
  return a / b; // DIVIDE
}

console.log(calculate("ADD",      10, 5));  // 15
console.log(calculate("SUBTRACT", 10, 5));  // 5
console.log(calculate("MULTIPLY", 10, 5));  // 50
console.log(calculate("DIVIDE",   10, 5));  // 2

try {
  calculate("DIVIDE", 10, 0);
} catch (error) {
  if (error instanceof Error) {
    console.log(error.message); // "Cannot divide by zero."
  }
}
```
