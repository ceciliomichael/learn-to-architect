# Module 20 Quiz Answers

## Answer 1

The parsed content is determined at runtime and may have any shape. `unknown` preserves that uncertainty until checks prove what it contains.

## Answer 2

`unknown` blocks most property access and calls until narrowing. `any` permits them and lets unchecked types flow onward.

## Answer 3

Check that its runtime type is object, that it is not null, and that it is not an array when arrays are not accepted.

## Answer 4

It is a type predicate. A true return gives TypeScript evidence to narrow the checked value to `User`.

## Answer 5

No. It is a static assertion only and emits no validator or conversion.
