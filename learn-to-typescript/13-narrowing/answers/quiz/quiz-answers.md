# Module 13 Quiz Answers

## Answer 1

The runtime value might be a number, and numbers do not have that string method. The operation is not safe for every union member.

## Answer 2

TypeScript narrows it to `number` inside the block.

## Answer 3

It returns `"object"`. Code checking objects must handle `null` separately.

## Answer 4

Zero is false-like in a condition, so the code would treat valid zero data as missing.

## Answer 5

Use `Array.isArray(value)`. It is a runtime check that TypeScript understands for narrowing.
