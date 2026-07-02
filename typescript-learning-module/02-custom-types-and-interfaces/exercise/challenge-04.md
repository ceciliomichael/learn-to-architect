# Challenge 04: Union Types in Action

Sometimes a single variable needs to hold different types of data at different times, like a user ID that can be either text or a number.

## Your Tasks

1. Create a `type` alias called `UserId` that allows either a `string` or a `number`.

2. Declare a variable named `currentId` using `let` and type it as `UserId`. Assign it a starting string value (for example, `"user-123"`).

3. Write an `if` statement using `typeof` to check if `currentId` is a `"string"`. Inside the `if` block, log the ID in uppercase using `.toUpperCase()`.

4. Next, change the value of `currentId` to a number (for example, `404`). Notice that TypeScript allows this without any errors because `currentId` allows both strings and numbers.

5. Write another `if` statement using `typeof` to check if `currentId` is now a `"number"`. Inside the block, log `"Numeric ID: " + currentId`.

## ANSWER HERE

```typescript
// Write your solution here


```
