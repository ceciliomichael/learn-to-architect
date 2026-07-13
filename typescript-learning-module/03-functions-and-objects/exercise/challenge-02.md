# Challenge 02: Optional and Default Parameters

Practice two kinds of flexible function parameters.

## Your Tasks

**Function 1: `greetOptional`**
- Parameters: `name: string`, `title?: string` (optional)
- Returns: `string`
- If `title` is provided, return `"Hello, [title] [name]"`.
- If not, return `"Hello, [name]"`.
- Use template literals (backtick strings with `${ }`).

**Function 2: `greetDefault`**
- Parameters: `name: string`, `title: string = "Traveler"` (default)
- Returns: `string`
- Always returns `"Hello, [title] [name]"`.

Call each function twice: once passing both arguments, once passing only the name. Log all four results and note which version of the greeting appears each time.

## ANSWER HERE

```typescript
// Write both greet functions and their calls here

function greetOptional(name: string, title? : string): string {
    if (title !== undefined) {
        return `Hello, ${title} ${name}`
    }
    else {
        return `Hello, ${name}`
    }
}

function greetDefault(name: string, title: string = "Traveler"): string {
    return `Hello, ${title} ${name}`
}

const optionalWithTitle: string = greetOptional("Robert", "Doctor")
const optionalWithoutTitle: string = greetOptional("Robert")
const defaultWithTitle: string = greetDefault("Robert", "Nurse")
const defaultWithoutTitle: string = greetDefault("Robert")

console.log(optionalWithTitle) // returns Hello, Doctor Robert
console.log(optionalWithoutTitle) // returns Hello, Robert
console.log(defaultWithTitle) // returns Hello, Nurse Robert
console.log(defaultWithoutTitle) // returns Hello, Traveler Robert
```
