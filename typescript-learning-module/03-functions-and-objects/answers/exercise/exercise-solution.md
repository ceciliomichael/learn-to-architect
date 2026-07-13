# Module 03 Exercise Solutions: Master Reference

Welcome to the production-grade solution guide for **Module 03: Functions and Signatures**. This document provides an exhaustive architectural review, complete code implementations, and deep technical trade-offs for all four practical lab challenges.

---

## 1. Solution Overview and Architectural Goals

In enterprise TypeScript engineering, functions are the foundational building blocks of computation. A well-designed function signature acts as an unbreakable contract between different modules, teams, and microservices. Throughout these solutions, we emphasize:

1. **Strict Type Safety**: Eliminating runtime type errors by leveraging literal unions, explicit return types, and array type annotations.
2. **Defensive Programming**: Validating boundaries and throwing meaningful runtime exceptions before corrupt state propagates across system pipelines.
3. **Declarative vs. Imperative Trade-Offs**: Understanding precisely when to use functional array transformation chains (`.filter()`, `.map()`, `.forEach()`) versus imperative control loops (`for...of`).

---

## 2. Challenge 01: Typed Calculator Function

### Complete Production Implementation

```typescript
type MathOperation = "ADD" | "SUBTRACT" | "MULTIPLY" | "DIVIDE";

function calculate(operation: MathOperation, a: number, b: number): number {
  switch (operation) {
    case "ADD":
      return a + b;
    case "SUBTRACT":
      return a - b;
    case "MULTIPLY":
      return a * b;
    case "DIVIDE":
      if (b === 0) {
        throw new Error("Cannot divide by zero.");
      }
      return a / b;
  }
}

// Verification and Testing
console.log("ADD Result:", calculate("ADD", 10, 5));           // Outputs: 15
console.log("SUBTRACT Result:", calculate("SUBTRACT", 10, 5)); // Outputs: 5
console.log("MULTIPLY Result:", calculate("MULTIPLY", 10, 5)); // Outputs: 50
console.log("DIVIDE Result:", calculate("DIVIDE", 10, 5));     // Outputs: 2

// Error Handling Demonstration
try {
  calculate("DIVIDE", 10, 0);
} catch (error) {
  if (error instanceof Error) {
    console.log("[RUNTIME EXCEPTION CAUGHT]:", error.message);
  }
}
```

### Architectural Trade-Offs
* **Literal Unions vs. Generic Strings**: Typing `operation` as `"ADD" | "SUBTRACT" | "MULTIPLY" | "DIVIDE"` prevents typos at compile time. If a developer calls `calculate("add", 10, 5)`, TypeScript blocks the build immediately.
* **Explicit Return Annotation**: Annotating `: number` guarantees that all branch paths return a numeric value. If a developer adds a new case without returning a number, the compiler flags the missing return.

---

## 3. Challenge 02: Optional and Default Parameters

### Complete Production Implementation

```typescript
function greetOptional(name: string, title?: string): string {
  if (title !== undefined) {
    return `Hello, ${title} ${name}`;
  }
  return `Hello, ${name}`;
}

function greetDefault(name: string, title: string = "Traveler"): string {
  return `Hello, ${title} ${name}`;
}

// Verification and Testing
console.log(greetOptional("Alice", "Dr."));  // Outputs: "Hello, Dr. Alice"
console.log(greetOptional("Alice"));          // Outputs: "Hello, Alice"

console.log(greetDefault("Bob", "Captain")); // Outputs: "Hello, Captain Bob"
console.log(greetDefault("Bob"));            // Outputs: "Hello, Traveler Bob"
```

### Architectural Trade-Offs
* **Optional vs. Default**: Use optional parameters (`?`) when the absence of a value carries semantic meaning (e.g., no title exists). Use default parameters (`=`) when a standard fallback is required for system operation.
* **Parameter Ordering**: In JavaScript runtime execution, arguments are assigned positionally from left to right. Placing required parameters after optional ones would make caller intent ambiguous; therefore, TypeScript mandates that optional parameters appear at the very end of the signature.

---

## 4. Challenge 03: Array Transformation Pipeline

### Complete Production Implementation

```typescript
interface Product {
  name: string;
  price: number;
  inStock: boolean;
}

const products: Product[] = [
  { name: "Sword",   price: 150, inStock: true  },
  { name: "Potion",  price: 25,  inStock: false },
  { name: "Shield",  price: 200, inStock: true  },
  { name: "Arrow",   price: 5,   inStock: true  },
  { name: "Helmet",  price: 175, inStock: false }
];

// Step 1: Filter to only available inventory
const availableProducts: Product[] = products.filter(
  (product: Product) => product.inStock === true
);

// Step 2: Map to formatted display labels
const productLabels: string[] = availableProducts.map(
  (product: Product) => `${product.name}: $${product.price}`
);

// Step 3: Execute side effects via forEach
productLabels.forEach((label: string) => {
  console.log(label);
});

// Step 4: Output inventory count
console.log("Total Available Products:", availableProducts.length);
```

### Architectural Trade-Offs
* **Declarative Pipelines vs. Imperative Loops**: As discussed in Section 8 of the README, `.filter()`, `.map()`, and `.forEach()` provide immutable, highly readable transformation pipelines. Every transformation step produces a clean intermediate array without mutating source data.
* **When to use `for...of`**: If this pipeline needed to abort early upon finding a specific product (using `break`) or execute asynchronous database saves sequentially (`await`), a `for...of` loop would be mandatory.

---

## 5. Challenge 04: Rest Parameters

### Complete Production Implementation

```typescript
function calculateTotal(...numbers: number[]): number {
  let total: number = 0;
  for (let num of numbers) {
    total = total + num;
  }
  return total;
}

function joinWords(...words: string[]): string {
  let result: string = "";
  for (let i = 0; i < words.length; i++) {
    if (i === 0) {
      result = words[i];
    } else {
      result = result + " " + words[i];
    }
  }
  return result;
}

// Verification and Testing
console.log("Total Sum:", calculateTotal(10, 20, 30, 40, 50)); // Outputs: 150
console.log("Joined String:", joinWords("TypeScript", "is", "really", "great")); // Outputs: "TypeScript is really great"
```

### Architectural Trade-Offs
* **Rest Parameters vs. Array Passing**: Designing `calculateTotal(...numbers: number[])` allows callers to pass comma-separated arguments natively (`calculateTotal(1, 2, 3)`). Under the hood, the JavaScript engine bundles these into a standard Array.
* **Iteration Mechanics**: In `calculateTotal`, using a `for...of` loop eliminates indexing errors and improves readability when accumulating mathematical sums.

---

## 6. Next Steps

To examine symbol-by-symbol breakdowns and deeper conceptual trade-offs for each challenge, consult the individual solution files in this directory:
* [Challenge 01 Solution](./challenge-01-solution.md)
* [Challenge 02 Solution](./challenge-02-solution.md)
* [Challenge 03 Solution](./challenge-03-solution.md)
* [Challenge 04 Solution](./challenge-04-solution.md)
