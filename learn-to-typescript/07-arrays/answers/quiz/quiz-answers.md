# Module 07 Quiz Answers

## Answer 1

The first index is `0`, the final index is `2`, and the length is `3`.

## Answer 2

It can return `undefined` because an empty array has no final item to remove.

## Answer 3

No. `const` prevents assigning a different array to `values`, but it does not make the existing array readonly. `push(3)` changes the existing array.

## Answer 4

```text
9
```

The loop adds `2`, `3`, and `4` to the running total.

## Answer 5

The requested position might not exist. JavaScript returns `undefined` for a missing index. A strict compiler option can include that possibility in the type, but runtime data still needs careful handling.
