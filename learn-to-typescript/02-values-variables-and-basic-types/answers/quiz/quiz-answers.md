# Module 02 Quiz Answers

## Answer 1

- Use `const` for the birth year because it is not reassigned.
- Use `let` for the score because it receives new values.
- Use `const` for the course title because it is not reassigned.

Choose based on whether the variable needs reassignment in this program, not based only on the real-world subject.

## Answer 2

- `"42"` is a string.
- `42` is a number.
- `false` is a boolean.
- `"false"` is a string.

Quotation marks create text.

## Answer 3

```text
3
number
```

The variable is updated before either print statement. `typeof` reports the runtime category `number`.

## Answer 4

TypeScript inferred `price` as a number from its first value. Assigning the string `"fifty"` does not match that type.

## Answer 5

```typescript
const isOpen = true;
console.log(typeof isOpen);
```

The output is `boolean`. Removing the quotation marks changes the value from text to a real boolean.
