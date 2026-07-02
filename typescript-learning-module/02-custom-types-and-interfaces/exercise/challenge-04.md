# Challenge 04: Union Types in Action

A function in your application needs to accept either a string ID or a numeric ID.

## Your Tasks

1. Create a `type` alias called `UserId` that is `string | number`.

2. Declare two variables using `UserId`: one assigned a string value and one assigned a number value.

3. Write a function called `printId(id: UserId): void` that
   - Uses `typeof` inside an `if/else` to check which type `id` is.
   - If it is a `string`: logs the id converted to uppercase.
   - If it is a `number`: logs `"ID: " + id`.

4. Call `printId` with both your string and number variables and verify the output.

## ANSWER HERE

```typescript
// Write your UserId type, variables, and printId function here
```
