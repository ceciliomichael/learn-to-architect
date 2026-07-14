# Module 06 Exercises

## Warm-up: A reusable greeting

Write a function named `greetLearner` that accepts a string parameter named `name` and prints a greeting. Call it with three different names.

## Guided exercise: Convert minutes

Write `convertHoursToMinutes`.

1. It accepts a number named `hours`.
2. It returns `hours * 60`.
3. Call it with `2` and store the result.
4. Print `2 hours is 120 minutes.` using the result.

## Independent exercise: Calculate a discounted price

Write a function named `calculateDiscountedPrice` with two number parameters:

- `price`
- `discountPercent`

It should calculate and return the price after the discount.

For a price of `1000` and a discount of `15`, the returned value should be `850`.

Call the function with at least two different sets of values.

## Decision exercise: Check a range

Write `isWithinRange`. It accepts `value`, `minimum`, and `maximum`, all numbers. It returns `true` when the value is at least the minimum and at most the maximum.

Test these calls:

```typescript
console.log(isWithinRange(5, 1, 10));
console.log(isWithinRange(12, 1, 10));
```

Expected output:

```text
true
false
```

## Debugging task

Fix the function so the final line prints `15`:

```typescript
function addNumbers(left: number, right: number) {
  const result = left + right;
  console.log(result);
}

const answer = addNumbers(7, 8);
console.log(answer);
```

Explain why the original final line did not contain the calculated number.

## Completion checklist

- [ ] I declared and called a function.
- [ ] I passed arguments that matched the parameter types.
- [ ] I returned a value used by later code.
- [ ] I kept local values inside their function.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
