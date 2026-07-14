# Module 10 Quiz Answers

## Answer 1

- A is a syntax problem.
- B is a type problem.
- C is a runtime problem in the described compiler conditions.
- D is a logic problem.

## Answer 2

Write down the input, expected output, and actual output. These facts make the mismatch specific.

## Answer 3

One early mistake can confuse the parser or type checker and create several later messages. Fixing the first clear cause may remove the later symptoms.

## Answer 4

Test `17`, `18`, and `19`. These values cover one below, exactly at, and one above the boundary.

## Answer 5

Print the total and current item immediately before the update, then print the total immediately after it. For example:

```typescript
console.log(`Before: total=${total}, value=${value}`);
total = total + value;
console.log(`After: total=${total}`);
```

The changing values reveal whether each repetition keeps earlier work or replaces it.
