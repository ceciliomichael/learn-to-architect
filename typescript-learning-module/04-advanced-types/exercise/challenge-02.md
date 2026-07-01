# Challenge 02: Discriminated Union State Machine

Model the different states of a file operation using a discriminated union.

## Your Tasks

1. Define a discriminated union type called `FileOperationResult` with three members:
   - `{ status: "idle" }`
   - `{ status: "processing"; filename: string; progress: number }`
   - `{ status: "complete"; filename: string; sizeBytes: number }`

2. Write a function `reportStatus(state: FileOperationResult): string` that uses a `switch` statement on `state.status` and returns a different message for each case:
   - `"idle"`: return `"No operation running."`
   - `"processing"`: return `"Processing [filename]: [progress]% done."`
   - `"complete"`: return `"[filename] completed. Size: [sizeBytes] bytes."`

3. Add a `default` case with a `never` exhaustiveness check.

4. Create one object for each state and test all three.

## ANSWER HERE

```typescript
// Write your discriminated union and reportStatus function here:


```
