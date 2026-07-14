# Module 09 Quiz Answers

## Answer 1

- Use `map` to create one label for every product.
- Use `filter` to keep only completed tasks.
- Use `find` to get the first score above 90.
- Use `some` to ask whether any item is unavailable.

## Answer 2

`forEach` returns `undefined`. Its purpose is to perform an action for each item, not to build a new array.

## Answer 3

No array item may satisfy the callback condition. In that case there is no matching value to return.

## Answer 4

```text
[20, 40]
```

`filter` keeps `2` and `4`. `map` then multiplies each kept value by 10.

## Answer 5

The callback block needs `return`:

```typescript
const doubled = [1, 2, 3].map((value) => {
  return value * 2;
});
```

Without it, every callback result is `undefined`.
