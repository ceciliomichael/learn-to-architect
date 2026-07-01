# Challenge 03: Safe Unknown Input

Working with `unknown` forces you to verify a value's type before using it. This is the safe way to handle data whose type you cannot guarantee in advance.

## Your Tasks

1. Declare a variable called `serverResponse` typed as `unknown` and assign it the string value `"Connection established"`.
2. Write an `if` statement using `typeof` that checks whether `serverResponse` is a string.
3. Inside the `if` block, log `serverResponse` converted to uppercase using `.toUpperCase()`.
4. Outside the `if` block, write a commented-out line that attempts to call `.toUpperCase()` directly on `serverResponse`. In the comment, write the TypeScript error message that would appear.
5. Change the value of `serverResponse` to the number `500`. Update your `if` statement to also check if it is a number, and in that branch log `"Error code: " + serverResponse`.

## ANSWER HERE

```typescript
// Write your unknown variable and typeof checks here:


```
