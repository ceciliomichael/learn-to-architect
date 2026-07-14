# Module 16 Exercises

## Exercise 1: Coordinate tuple

Create a labeled, readonly tuple type named `Coordinate` with number positions `x` and `y`. Create a coordinate, destructure it, and print both values.

## Exercise 2: Result pair

Create `type NameAndLength = [name: string, length: number]`. Write a function that accepts a string and returns this tuple. Test it with `"TypeScript"`.

## Exercise 3: Readonly input

Write `findMaximum(values: readonly number[]): number | undefined`. Return undefined for an empty array. Do not mutate the input.

## Exercise 4: Choose the structure

Choose array, tuple, or object for each and explain:

- all temperatures recorded during a month
- latitude and longitude as two ordered values
- a customer with name, email, and optional phone
- a pair containing a label and numeric count

## Exercise 5: Repair a mutation contract

This function only needs to read names. Change its input type so it also accepts a readonly array:

```typescript
function firstName(names: string[]): string | undefined {
  return names[0];
}
```

## Completion checklist

- [ ] I created and destructured a tuple.
- [ ] I used readonly on a collection input.
- [ ] I handled an empty array result.
- [ ] I chose structures based on meaning.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
