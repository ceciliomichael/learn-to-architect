# Challenge 03 Solution: The Result Pattern & Discriminated Unions

## Executive Summary & Architectural Overview

In traditional object-oriented programming, throwing exceptions (`throw new Error(...)`) is the default mechanism for handling failures. However, in enterprise software architecture, throwing exceptions for *expected operational failures* (such as invalid user input, missing database records, or insufficient bank balance) introduces serious problems:
1. **Hidden Control Flow:** Function signatures like `function getUser(): Promise<User>` do not document what exceptions might be thrown. Callers must inspect source code or documentation to know what `try / catch` blocks to write.
2. **Performance Overhead:** Throwing exceptions forces the JavaScript runtime to perform stack unwinding and trace generation, which is computationally expensive.
3. **Unhandled Crash Risks:** If a developer forgets to wrap a call in a `try / catch` block, the exception bubbles up and can crash the server process or freeze the user interface.

Functional programming architectures solve this by introducing the **Result Pattern** (`Result<T, E>`). Instead of throwing exceptions, functions return a **Discriminated Union** that explicitly represents either success or failure. This solution demonstrates how to build and consume type-safe Result monads in TypeScript.

---

## Production-Grade Implementation

```typescript
/**
 * Represents a successful operation containing a typed data payload.
 */
export type Ok<T> = {
  readonly success: true; // Discriminator Tag
  readonly data: T;
};

/**
 * Represents a failed operation containing a typed error explanation.
 */
export type Err<E> = {
  readonly success: false; // Discriminator Tag
  readonly error: E;
};

/**
 * The Discriminated Union representing the outcome of an operation.
 * Functions return Result<T, E> instead of throwing runtime exceptions.
 */
export type Result<T, E = string> = Ok<T> | Err<E>;

// ==========================================
// Helper Constructor Functions
// ==========================================

/**
 * Creates a sealed success object (Ok pouch).
 */
export function createOk<T>(data: T): Ok<T> {
  return { success: true, data };
}

/**
 * Creates a sealed failure object (Err pouch).
 */
export function createErr<E>(error: E): Err<E> {
  return { success: false, error };
}

// ==========================================
// Domain Logic Using the Result Pattern
// ==========================================

/**
 * Safely divides two numbers without ever throwing a division-by-zero exception.
 */
function divideNumbers(a: number, b: number): Result<number, string> {
  if (b === 0) {
    // Return a failure object instead of throwing!
    return createErr("Cannot divide by zero. Denominator must be non-zero.");
  }
  
  // Return a success object containing the quotient
  return createOk(a / b);
}

/**
 * Safely parses and validates an age input string without throwing NaN exceptions.
 */
function parseAge(input: string): Result<number, string> {
  // Attempt to parse integer using base 10
  const age = parseInt(input, 10);
  
  // Rule 1: Must be a valid numeric NaN check
  if (Number.isNaN(age)) {
    return createErr(`Not a valid number: '${input}' cannot be parsed into an integer.`);
  }
  
  // Rule 2: Must be within realistic biological bounds
  if (age < 1 || age > 120) {
    return createErr(`Age out of bounds: Must be between 1 and 120 (received ${age}).`);
  }
  
  return createOk(age);
}

// ==========================================
// Verification & Test Executions
// ==========================================

function testDivision(a: number, b: number): void {
  console.log(`\n--- Executing: divideNumbers(${a}, ${b}) ---`);
  const outcome = divideNumbers(a, b);
  
  // Inspect the discriminator tag!
  if (outcome.success) {
    // Inside this block, TypeScript narrows 'outcome' strictly to Ok<number>!
    // We can safely access outcome.data! Accessing outcome.error would be a compiler error!
    console.log(`[SUCCESS]: Quotient is ${outcome.data}`);
  } else {
    // Inside this block, TypeScript narrows 'outcome' strictly to Err<string>!
    // We can safely access outcome.error! Accessing outcome.data would be a compiler error!
    console.warn(`[FAILURE]: Operation blocked -> ${outcome.error}`);
  }
}

function testAgeParsing(input: string): void {
  console.log(`\n--- Executing: parseAge("${input}") ---`);
  const outcome = parseAge(input);
  
  if (outcome.success) {
    console.log(`[SUCCESS]: Valid age registered -> ${outcome.data} years old.`);
  } else {
    console.warn(`[VALIDATION ERROR]: ${outcome.error}`);
  }
}

// Execute division tests
testDivision(100, 4); // Success case -> 25
testDivision(50, 0);  // Failure case -> Cannot divide by zero

// Execute age parsing tests
testAgeParsing("28");           // Success case -> 28
testAgeParsing("not-a-number"); // Failure case -> Not a valid number
testAgeParsing("150");          // Failure case -> Out of bounds
testAgeParsing("-5");           // Failure case -> Out of bounds
```

---

## Symbol-by-Symbol Breakdown

1. **`readonly success: true`**: The **Discriminator Tag** (also known as the literal tag or discriminant property). By assigning a literal boolean type (`true` or `false`) to a shared property name across union members, we enable TypeScript's compiler to perform **Control Flow Based Type Narrowing**.
2. **`Result<T, E = string>`**: A generic type definition. `T` represents the type of the successful payload (e.g., `number`, `User`, `Order`), while `E` represents the error type (defaulting to `string`, but can be typed as a custom domain error class or union of error codes).
3. **`createOk(data)` & `createErr(error)`**: Factory functions (monadic constructors). They wrap raw values inside structured objects with the correct boolean discriminator tag. This eliminates repetitive object literal typing and prevents accidental tag misassignment.
4. **`if (outcome.success)`**: The narrowing gate. When this boolean evaluation is true, the TypeScript type checker eliminates `Err<E>` from the union, narrowing `outcome` strictly to `Ok<T>`. When false, it eliminates `Ok<T>`, narrowing `outcome` strictly to `Err<E>`.
5. **`Number.isNaN(age)`**: The modern, safe static method for checking if a value is `NaN`. Unlike global `isNaN()`, `Number.isNaN()` does not perform aggressive type coercion before checking.

---

## Runtime Performance & V8 Engine Optimization

### 1. Avoiding Stack Unwinding Overhead
When a JavaScript engine encounters a `throw new Error(...)` statement, normal execution stops immediately. The runtime initiates **Stack Unwinding**:
- It suspends the current stack frame.
- It walks backward through the call stack to construct a formatted stack trace string.
- It searches for an enclosing exception handler (`try / catch`).
- If no handler is found in the immediate frame, it pops the frame and inspects the caller frame, repeating until a handler is found or the process crashes.

In high-throughput systems (such as a Node.js API server processing thousands of financial transactions per second), if 15% of transactions fail due to routine validation errors (like insufficient funds or invalid PINs), throwing exceptions for those routine failures creates severe CPU deoptimization!

### 2. Heap Allocation vs. Stack Unwinding
By returning a `Result<T, E>` object, operational failures are treated as standard function return values:
- The V8 engine simply allocates a small, lightweight plain JavaScript object on the heap (`{ success: false, error: "..." }`).
- Zero stack trace strings are generated or formatted.
- Zero stack frames are unwound or inspected.
- Control flow proceeds linearly, allowing V8's JIT (Just-In-Time) compiler to optimize the code path aggressively without deoptimizing around exception handlers!

---

## Architectural Trade-offs: Result Pattern vs. Traditional `try / catch`

| Feature / Dimension | The Result Pattern (`Result<T, E>`) | Traditional Exception Throwing (`try / catch`) |
| :--- | :--- | :--- |
| **Type Safety & Signature Clarity** | **100% Explicit:** Signatures explicitly declare both success and failure types (`Result<User, AuthError>`). | **Hidden:** Signatures only declare success types (`Promise<User>`). Failures are invisible in types. |
| **Control Flow & Readability** | **Linear & Predictable:** Code reads smoothly from top to bottom; branching is handled via standard `if / else` statements. | **Non-Linear:** Control jumps abruptly from the `throw` statement to the nearest `catch` block across scopes. |
| **Runtime Performance** | **Extremely Fast:** Allocates lightweight plain objects; zero stack trace generation or unwinding overhead. | **Heavy Overhead:** Generates stack traces and unwinds stack frames upon throwing. |
| **Boilerplate & Verbosity** | **Moderate Verbosity:** Requires checking `.success` tags at each operational step before using values. | **Low Boilerplate in Happy Path:** Logic can be written sequentially without checking intermediate error states. |
| **Best Architectural Use Case** | Expected operational domain failures (validation errors, missing database records, business rule rejections, parsing errors). | Truly exceptional, unexpected system crashes (database connection loss, out-of-memory errors, hardware failures). |

---

## Concrete Anti-Patterns vs. Best Practices

### 1. Throwing Exceptions for Expected Domain Validation (Anti-Pattern)
```typescript
// ANTI-PATTERN: Using exception throwing for routine business validation!
function withdrawMoney(balance: number, amount: number): number {
  if (amount > balance) {
    // This is an expected business event, NOT an unexpected system crash!
    // Throwing forces all callers to wrap in try / catch!
    throw new Error("Insufficient funds");
  }
  return balance - amount;
}

// BEST PRACTICE: Using Result Pattern for expected domain outcomes
function withdrawMoneySafe(balance: number, amount: number): Result<number, string> {
  if (amount > balance) {
    return createErr("Insufficient funds for withdrawal.");
  }
  return createOk(balance - amount);
}
```

### 2. Using Ambiguous Tuples Instead of Discriminated Unions (Anti-Pattern)
```typescript
// ANTI-PATTERN: Go-style ambiguous tuples without discriminators
function getData(): [any, Error | null] {
  if (failed) return [null, new Error("Failed")];
  return [{ id: 1 }, null];
}
// Problem: TypeScript cannot narrow the first element based on checking the second element!
const [data, err] = getData();
if (!err) {
  // data is still 'any' or nullable! No automatic type narrowing!
}

// BEST PRACTICE: Discriminated Unions with boolean tags
function getDataSafe(): Result<{ id: number }, string> {
  if (failed) return createErr("Failed");
  return createOk({ id: 1 });
}
const outcome = getDataSafe();
if (outcome.success) {
  // TypeScript automatically narrows outcome.data to { id: number }!
}
```

### 3. Forgetting to Check the Discriminator Tag Before Accessing Data
```typescript
// ANTI-PATTERN: Attempting to access .data without checking .success
const outcome = divideNumbers(10, 2);
// Compiler Error in strict mode: Property 'data' does not exist on type 'Err<string>'!
console.log(outcome.data);

// BEST PRACTICE: Always narrow via the discriminator tag first
const outcomeSafe = divideNumbers(10, 2);
if (outcomeSafe.success) {
  console.log(outcomeSafe.data); // Safely unlocked!
} else {
  console.error(outcomeSafe.error); // Safely unlocked!
}
```
