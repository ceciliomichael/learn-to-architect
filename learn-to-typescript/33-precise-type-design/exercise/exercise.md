# Module 33 Exercises

## Exercise 1: Derive a literal union

Create a readonly tuple of three permission names with `as const`. Derive the union using `(typeof permissions)[number]`.

## Exercise 2: Check a complete mapping

Use `satisfies` to check that every permission has a display label. Misspell one key, observe the error, then fix it.

## Exercise 3: Compare annotation and satisfies

Create the same route object once with `Record<string, string>` annotation and once with `satisfies Record<string, string>`. Inspect the known key information in the editor and explain the difference.

## Exercise 4: Validate a branded id

Create `ProductId` for strings beginning with `product_`. Write one parsing function and one function that accepts only `ProductId`.

## Exercise 5: Callback safety

Explain why a function that requires a `Dog` cannot be used where a caller may pass any `Animal`. Then write a handler that accepts all Animals.

## Completion checklist

- [ ] I derived a literal union from a value.
- [ ] I used `satisfies` as a check, not conversion.
- [ ] I created a brand only after validation.
- [ ] I reasoned from what a callback caller may pass.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
