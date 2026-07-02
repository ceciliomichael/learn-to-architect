# Challenge 03: Generic Interface with Default Type

Build a reusable API response wrapper using a generic interface.

## Your Tasks

1. Create a generic interface `ApiResponse<T = string>` with
   - `success: boolean`
   - `data: T`
   - `errorMessage: string | null`

2. Create three typed variables using this interface
   - `textResponse`: uses the default `T = string`. Assign a real response object.
   - `numberResponse`: uses `T = number`. Assign a real response object.
   - `userResponse`: uses `T = { id: number; username: string }`. Assign a real response object.

3. For `textResponse`, write what TypeScript infers as the type of `.data` in a comment.
4. For `userResponse`, access and log `.data.username`.

## ANSWER HERE

```typescript
// Write your ApiResponse interface and three response variables here
```
