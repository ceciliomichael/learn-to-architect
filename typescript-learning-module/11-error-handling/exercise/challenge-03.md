# Challenge 03: The Result Pattern

In functional programming architectures (popularized by Rust, Go, and Elm), engineers avoid throwing runtime exceptions for expected operational failures. Throwing exceptions breaks linear control flow, requires expensive stack unwinding, and creates unhandled crash risks. 

Instead, functions return a Discriminated Union called the **Result Pattern** (`Result<T, E>`). The returned object explicitly contains either a success payload or a failure explanation, allowing the compiler to enforce comprehensive error handling without `try / catch` blocks.

## Your Tasks

1. Create a generic discriminated union `type Result<T, E = string>` that represents one of two possible states:
   - **Success State:** `{ readonly success: true; readonly data: T }`
   - **Failure State:** `{ readonly success: false; readonly error: E }`

2. Write a mathematical function `divideNumbers(a: number, b: number): Result<number>` that:
   - Returns `{ success: false, error: "Cannot divide by zero." }` if `b === 0`.
   - Returns `{ success: true, data: a / b }` otherwise.

3. Write an input validation function `parseAge(input: string): Result<number>` that:
   - Converts `input` to an integer using `parseInt(input, 10)`.
   - Returns failure if the parsed value is `NaN` (not a valid number) with message: `"Not a valid number."`.
   - Returns failure if the number is less than 1 or greater than 120 with message: `"Age must be between 1 and 120."`.
   - Returns success with the parsed number otherwise.

4. Test your implementation by executing both functions with success and failure inputs:
   - Store the returned result in a variable.
   - Use an `if (result.success)` check to narrow the discriminated union.
   - Log `result.data` on success and `result.error` on failure. Notice how TypeScript unlocks the correct property automatically based on the `.success` discriminator!

## ANSWER HERE

```typescript
// Write Result<T, E>, divideNumbers, parseAge, and test executions here
```
