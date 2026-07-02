# Challenge 03: The Result Pattern

Model success and failure as data instead of exceptions.

## Your Tasks

1. Create a generic `type Result<T>` that is either
   - `{ success: true; data: T }` (success branch)
   - `{ success: false; error: string }` (failure branch)

2. Write a function `divideNumbers(a: number, b: number): Result<number>` that
   - Returns `{ success: false, error: "Cannot divide by zero." }` if `b === 0`.
   - Returns `{ success: true, data: a / b }` otherwise.

3. Write a function `parseAge(input: string): Result<number>` that
   - Converts `input` to a number using `parseInt(input)`.
   - Returns failure if the result is `NaN` (not a valid number) with message `"Not a valid number."`.
   - Returns failure if the number is less than 1 or greater than 120 with message `"Age must be between 1 and 120."`.
   - Returns success with the parsed number otherwise.

4. Test each function with both a success case and a failure case. Use `if (result.success)` to branch and log different output.

## ANSWER HERE

```typescript
// Write Result<T>, divideNumbers, and parseAge here
```
