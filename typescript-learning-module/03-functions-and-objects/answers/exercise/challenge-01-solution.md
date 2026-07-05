# Challenge 01 Solution: Typed Calculator Function

This document provides the exhaustive production-grade solution, symbol-by-symbol analysis, and architectural trade-offs for **Challenge 01: Typed Calculator Function**.

---

## 1. Complete Production Implementation

```typescript
type MathOperation = "ADD" | "SUBTRACT" | "MULTIPLY" | "DIVIDE";

function calculate(operation: MathOperation, a: number, b: number): number {
  if (operation === "DIVIDE" && b === 0) {
    throw new Error("Cannot divide by zero.");
  }

  switch (operation) {
    case "ADD":
      return a + b;
    case "SUBTRACT":
      return a - b;
    case "MULTIPLY":
      return a * b;
    case "DIVIDE":
      return a / b;
  }
}

// Verification and Testing
console.log(calculate("ADD", 10, 5));      // Outputs: 15
console.log(calculate("SUBTRACT", 10, 5)); // Outputs: 5
console.log("MULTIPLY:", calculate("MULTIPLY", 10, 5)); // Outputs: 50
console.log("DIVIDE:", calculate("DIVIDE", 10, 5));     // Outputs: 2

// Exception Handling Demonstration
try {
  calculate("DIVIDE", 10, 0);
} catch (error) {
  if (error instanceof Error) {
    console.log("[CAUGHT ERROR]:", error.message); // Outputs: "Cannot divide by zero."
  }
}
```

---

## 2. Symbol-by-Symbol Analysis

Let us deconstruct the function signature `function calculate(operation: MathOperation, a: number, b: number): number {`:

* `function`: Built-in TypeScript and JavaScript keyword initiating the declaration of a reusable executable code block.
* `calculate`: Developer-assigned identifier representing the action engine.
* `(`: Opening parenthesis defining the boundary of the input parameter list.
* `operation`: Identifier for the first parameter, representing the mathematical action to execute.
* `:` (first colon): Type annotation anchor binding the parameter to its required type contract.
* `MathOperation`: Custom literal union type restricting inputs strictly to `"ADD"`, `"SUBTRACT"`, `"MULTIPLY"`, or `"DIVIDE"`.
* `,`: Comma separator dividing parameter definitions.
* `a` and `b`: Developer-assigned identifiers for the numeric operands.
* `: number`: Type annotation requiring operands to be IEEE 754 floating-point numbers.
* `)`: Closing parenthesis marking the termination of the parameter list.
* `:` (final colon): Return type annotation anchor specifying the guaranteed output data format.
* `number` (return type): Enforces that the function must evaluate to and return a numeric value.
* `{`: Opening curly brace marking the beginning of the executable function body.

---

## 3. Architectural Trade-Offs and Best Practices

### Literal Union Types vs. Generic Strings
If we typed `operation: string`, a caller could pass `"add"`, `"plus"`, or `"SUM"`. Because standard strings are infinitely wide, typos would not be caught until runtime, leading to silent failures or unhandled cases. By defining `type MathOperation = "ADD" | "SUBTRACT" | "MULTIPLY" | "DIVIDE"`, the TypeScript compiler enforces an exact closed set of allowed values at compile time.

### Explicit Return Annotations vs. Type Inference
While TypeScript can infer the return type of `calculate` by inspecting the `return a + b` statements, senior engineers strictly require explicit return type annotations on public utility functions. If a developer modifies the switch statement in the future and accidentally forgets a return statement (causing an implicit return of `undefined`), the explicit `: number` annotation immediately triggers a compile error inside the function itself.

### Runtime Error Throwing vs. Special Return Values
In JavaScript, dividing by zero (`10 / 0`) evaluates to `Infinity`, while dividing zero by zero (`0 / 0`) evaluates to `NaN` (Not a Number). In financial or enterprise calculations, allowing `Infinity` or `NaN` to silently propagate through data pipelines causes catastrophic downstream corruption in accounting databases. Throwing an explicit runtime exception (`throw new Error("Cannot divide by zero.")`) halts execution immediately at the boundary of failure, enforcing defensive programming principles.
