# Module 34 Exercises

## Exercise 1: Runtime tests

Write and test `clamp(value, minimum, maximum)`. Test a middle value, both exact boundaries, one value below, and one above.

## Exercise 2: Error test

Write a function that throws for an empty required title. Use `assert.throws` to test it and also test a valid title.

## Exercise 3: Async test

Test a Promise-returning function for fulfillment and another for rejection. Ensure the test awaits both operations.

## Exercise 4: Type contract tests

Create `setStatus(status: "open" | "closed"): void`. Add valid calls and one invalid call guarded by `@ts-expect-error`. Temporarily widen the parameter to string and observe the unused-directive error.

## Exercise 5: Refactor safely

Choose one earlier exercise with at least two functions. Add runtime tests, run the type checker, rename or split one function, and use failures to update every caller. Record the check order you used.

## Exercise 6: Upgrade plan

Write a six-step plan for upgrading TypeScript in the Module 19 project. Include official release notes, a clean starting state, checking, tests, and review of new diagnostics.

## Completion checklist

- [ ] I tested runtime results and boundaries.
- [ ] I awaited asynchronous tests.
- [ ] I wrote an intentional negative type test.
- [ ] I refactored with small feedback loops.
- [ ] I planned an evidence-based dependency upgrade.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
