# Module 17 Quiz Answers

## Answer 1

An array is a named collection of related values stored in order. Each value is an element, and each element has a position called an index.

## Answer 2

**B.** Valid 0-based indexes for size 4 are `0`, `1`, `2`, and `3`.

## Answer 3

`19`

Indexes: `0 -> 18`, `1 -> 21`, `2 -> 19`, `3 -> 22`.

## Answer 4

A loop can use the same body for every index, such as `temps[index]`. Separate variable names force you to write nearly the same instruction many times and make it harder to change the count later.

## Answer 5

`names` has size 3, so valid indexes are `0`, `1`, and `2`. Index `3` is out of range.

A corrected line could be:

```text
OUTPUT names[2]
```

That prints `Sam`, the last name.
