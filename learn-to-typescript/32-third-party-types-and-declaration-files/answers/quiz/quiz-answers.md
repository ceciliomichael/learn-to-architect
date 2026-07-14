# Module 32 Quiz Answers

## Answer 1

They can be built into TypeScript's libraries, bundled with the package, supplied by a matching `@types` package, or written locally when necessary.

## Answer 2

No. It describes runtime code that must exist separately.

## Answer 3

Exports and values from the module become effectively unchecked `any`, so bad calls can pass type checking.

## Answer 4

The runtime library or plugin must actually provide behavior matching the augmented type declarations.

## Answer 5

It emits `.d.ts` files that describe exported APIs.
