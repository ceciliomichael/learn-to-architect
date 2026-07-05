# Module 01 Master Quiz Answers & Architectural Reference

## Executive Summary
This document serves as the verified, exhaustive master answer key and architectural reference for all conceptual quiz questions in Module 01 (The Basics). It corrects all previous reference mismatches, providing complete explanations, compiler mechanics, memory allocation models, and production design trade-offs for Questions 01 through 05.

Use this reference guide to validate your conceptual understanding and master the underlying mechanics of the TypeScript compiler and JavaScript runtime engine.

---

## Question 01: What Happens to Types at Runtime?

### Verified Correct Answer: Option B
**"They are completely removed and do not exist in the running JavaScript."**

### Comprehensive Explanation
TypeScript is strictly a **development-time static analysis tool**. When the TypeScript compiler (`tsc`) translates your `.ts` source code into `.js` files for execution in browsers or Node.js, it executes a process called **Type Erasure**.
During type erasure, every single type annotation (`: string`, `: number[]`, `interface`, `type`, `readonly`) is stripped away completely. The emitted JavaScript output contains zero type information, zero automatic `typeof` runtime checks, and zero overhead.

### Architectural Trade-Offs
* **Advantage (Zero Overhead):** Because types are erased at compile time, TypeScript adds zero runtime latency and consumes zero extra heap memory compared to standard JavaScript.
* **Trade-Off (No Runtime Enforcement):** Because types do not exist at runtime, TypeScript cannot stop external network requests or third-party libraries from sending corrupted data shapes during execution. You must implement runtime type guards (like `typeof` checks) at application boundaries to protect your system.

---

## Question 02: `const` and Arrays

### Verified Correct Answer
**No, TypeScript does NOT throw an error when calling `.push()` on a `const` array.**

### Comprehensive Explanation
To understand this behavior, you must separate variable bindings in stack memory from data structures in heap memory:
1. **The Stack Binding (`const scores`):** The keyword `const` locks down the variable pointer reference in stack memory. It forbids you from reassigning the variable label to point to a brand new memory address (for example, `scores = [100, 200]` throws a compiler error).
2. **The Heap Structure (`[90, 85]`):** The actual array contents reside in heap memory. Calling `scores.push(100)` does not reassign the stack pointer; it simply reaches along the existing pointer into heap memory and appends a new element into an open compartment slot. Because the pointer reference remains unchanged, `const` permits the internal mutation.

### True Deep Immutability (`as const`)
To freeze both the variable pointer and the internal heap array contents, use TypeScript's readonly assertion:
```typescript
const frozenScores = [90, 85] as const;
// frozenScores.push(100); // COMPILER ERROR: Property 'push' does not exist on type 'readonly [90, 85]'.
```

---

## Question 03: Type Inference

### Verified Correct Answers
1. **Why `city = 42` is rejected:** The compiler rejects assigning `42` because `42` is a numeric integer (`number`), whereas the variable `city` was permanently bound to textual data (`string`). TypeScript forbids assigning incompatible data types to existing containers.
2. **Why TypeScript knew the type without an explicit annotation:** When you declare and initialize a variable on the exact same line (`let city = "Tokyo";`), TypeScript executes **Type Inference**. It inspects the assigned literal value (`"Tokyo"`), identifies it as a string, and automatically attaches the `: string` contract to `city` in memory for its entire lifecycle.

### Architectural Best Practices
* **Internal Function Logic:** Rely on automatic Type Inference for local variables inside function bodies to keep code clean and readable without clutter.
* **Module and API Boundaries:** Always write explicit type annotations on function parameters, return types, and exported module constants. Explicit annotations act as architectural contracts that prevent internal implementation changes from silently breaking downstream consumers.

---

## Question 04: `any` vs `unknown`

### Verified Correct Answers
1. **Calling `.explode()` on `any` vs `unknown`:**
   * **`valueA: any`:** The compiler produces **zero errors** and allows the build to succeed. However, when executed at runtime, the program crashes with a fatal exception: `TypeError: valueA.explode is not a function`.
   * **`valueB: unknown`:** The compiler immediately blocks the build with an error: `Object is of type 'unknown'`. It strictly forbids calling methods or reading properties on quarantined data.
2. **Which type to prefer:** Always prefer **`unknown`**. It enforces a Zero Trust security model, requiring you to prove data types at compile time rather than suffering catastrophic runtime crashes.
3. **What you must do before using `unknown`:** You must perform a **Type Narrowing Check** (such as `if (typeof valueB === "string")`) to prove the runtime data shape before accessing type-specific methods.

### Enterprise Security Pattern
Never use `any` to silence compiler errors when parsing HTTP webhooks or JSON payloads. Always ingest external payloads into `unknown` containers and validate them using runtime `typeof` guards or schema validation libraries before executing database queries.

---

## Question 05: String Methods & Array Transformations

### Verified Complete Implementation
```typescript
// 1. Split comma-separated string into a typed string[] array
const rawData: string = "10,20,30";
const parts: string[] = rawData.split(","); // ["10", "20", "30"]

// 2. Access element using zero-based indexing offset
const secondItem: string = parts[1]; // "20"

// 3. Invoke string transformation method
console.log("Uppercase:", secondItem.toUpperCase()); // "20"

// 4. Convert textual string into a mathematical number
const numericValue: number = parseInt(secondItem);
console.log("Numeric Value:", numericValue); // 20
```

### Technical Breakdown & Production Traps
* **Zero-Based Indexing:** Array index offsets start at `0`. The second element always resides at index `1`.
* **Method Invocation vs. Properties:** Properties (like `.length`) represent stored attributes and are accessed without parentheses. Methods (like `.split()` or `.toUpperCase()`) represent executable actions and require parentheses `()` to trigger execution.
* **The `NaN` (Not a Number) Trap:** In production ingestion pipelines, calling `parseInt()` on invalid text (such as `"twenty"`) returns the special value `NaN`. In TypeScript, `typeof NaN` returns `"number"`, which can silently corrupt downstream mathematical calculations. Senior engineers always validate parsed integers using `isNaN(numericValue)` before executing business arithmetic.

---

## Master Summary Checklist

By completing Module 01, you have built the foundational architectural habits of senior TypeScript developers:
* You understand that TypeScript is a development-time safety net erased during compilation.
* You enforce immutability using `const` and `as const` appropriately across stack and heap allocations.
* You leverage Type Inference for clean internal logic while enforcing explicit type contracts at module boundaries.
* You implement Zero Trust data ingestion using `unknown` and runtime type narrowing instead of resorting to `any`.
* You manipulate primitive strings and arrays safely while guarding against production runtime pitfalls like `NaN`.
