# Module 21 Exercises

## Exercise 1: Throw an error

Write `getItemAt(items: readonly string[], index: number): string`. Throw an `Error` with a clear message when the item is missing. Catch it at the call site and narrow the caught value.

## Exercise 2: Result for validation

Create a result union for validating a positive number. Return `{ ok: true, value }` or `{ ok: false, error }`. Test zero, a negative number, and a positive number.

## Exercise 3: Safe JSON parsing

Write `parseJson` from the lesson without copying it. Test valid and invalid JSON. On success, keep the value typed as unknown.

## Exercise 4: Cleanup trace

Write a `try`, `catch`, and `finally` example that prints the order of each block for success and failure. Do not return from `finally`.

## Exercise 5: Expected or exceptional

Choose result or throw for each and explain:

- a password form does not meet visible length rules
- an internal function reaches a state its caller promised was impossible
- a search has no matching item
- a required configuration file cannot be read at program startup

## Completion checklist

- [ ] I threw an `Error` object.
- [ ] I narrowed a caught unknown value.
- [ ] I returned an explicit expected failure.
- [ ] I kept parsed JSON unknown until validation.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
