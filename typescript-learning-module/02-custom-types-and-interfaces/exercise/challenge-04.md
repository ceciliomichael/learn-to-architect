# Challenge 04: Union Types in Action

Your application stores user identifiers that can be either a text string or a numeric ID.

## Your Tasks

1. Create a `type` alias called `UserId` that is `string | number`.

2. Declare a variable using `let` called `currentId: UserId` and assign it a string value (e.g., `"user-abc"`).

3. Write an `if` check verifying that `typeof currentId === "string"`, and inside the block log `currentId.toUpperCase()`.

4. Next, reassign `currentId = 101;` (a number). Notice TypeScript allows this because `currentId` has the union type `string | number`.

5. Write an `if` check verifying that `typeof currentId === "number"`, and inside the block log `"Numeric ID: " + currentId`.

## ANSWER HERE

```typescript
// Write your UserId type, variables, and if/else checks here

```
