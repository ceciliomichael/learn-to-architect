# Challenge 04: Union Types in Action

Your application stores user identifiers that can be either a text string or a numeric ID.

## Your Tasks

1. Create a `type` alias called `UserId` that is `string | number`.

2. Declare two variables using `UserId`: one assigned a string value (e.g., `"user-abc"`) and one assigned a number value (e.g., `101`).

3. Write an `if/else` statement using `typeof` directly on your string variable:
   - If `typeof` equals `"string"`, log the ID converted to uppercase using `.toUpperCase()`.
   - If `typeof` equals `"number"`, log `"Numeric ID: " + value`.

4. Repeat the same `if/else` check on your number variable to verify that TypeScript safely narrows union types without using functions.

## ANSWER HERE

```typescript
// Write your UserId type, variables, and if/else checks here


```
