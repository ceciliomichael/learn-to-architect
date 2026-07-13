# Challenge 01: Typed Calculator Function

Write a strictly typed calculator that handles four operations.

## Your Tasks

Write a function called `calculate` with these parameters
- `operation`: typed as the literal union `'ADD' | 'SUBTRACT' | 'MULTIPLY' | 'DIVIDE'`
- `a`: a number
- `b`: a number
- Returns: a number

Rules
- If `operation` is `'DIVIDE'` and `b` is `0`, throw `new Error('Cannot divide by zero.')`.
- Otherwise, perform the correct math and return the result.

Call the function with all four operations and log each result. Also show what happens when you call `calculate('DIVIDE', 10, 0)` inside a `try/catch` and log the caught error message.

## ANSWER HERE

```typescript
// Write your calculate function here

function calculate(operation: 'ADD' | 'SUBTRACT' | 'MULTIPLY' | 'DIVIDE', a: number, b: number): number {
    if (operation === 'ADD') {
        return a + b
    }
    else if (operation === 'SUBTRACT') {
        return a - b
    } else if (operation === 'MULTIPLY') {
        return a * b
    } else {
        if (b === 0) {
            throw new Error('Cannot divide by zero.')
        }
        return a / b
    }
}

console.log(calculate('ADD', 5, 3)) // 8
console.log(calculate('SUBTRACT', 5, 6)) // -1
console.log(calculate('MULTIPLY', 5, 3)) // 15
console.log(calculate('DIVIDE', 10, 2)) // 5

try {
    console.log(calculate('DIVIDE', 10, 0))
}
catch (error) {
    if (error instanceof Error) {
        console.log(error.message)
    } else {
        console.log('An unknown error occurred.')
    }
}
```
