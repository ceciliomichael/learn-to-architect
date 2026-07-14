# Module 13 Exercises

## Exercise 1: Format mixed identifiers

Write `formatIdentifier(value: string | number): string`.

- Return an uppercase string when given a string.
- Return a number formatted with two decimal places when given a number.

Test both branches.

## Exercise 2: Handle a missing title

Write `printTitle(title: string | null): void`. If the value is `null`, print `No title`. Use an early return. Otherwise print the uppercase title.

## Exercise 3: Handle text or a text list

Write `firstText(input: string | string[]): string | undefined`.

- For a string, return the whole string.
- For an array, return its first item.

Remember that an empty array has no first item.

## Exercise 4: Repair a truthiness bug

The value `0` is a valid measurement and should print. Fix the function:

```typescript
function printMeasurement(value: number | undefined): void {
  if (value) {
    console.log(value);
  } else {
    console.log("Missing measurement");
  }
}
```

Test `0`, `5`, and `undefined`.

## Exercise 5: Narrow different object shapes

Create:

```typescript
type FileMessage = { fileName: string };
type TextMessage = { text: string };
```

Write a function that uses `"fileName" in message` to return either `File: name` or `Text: content`.

## Completion checklist

- [ ] I narrowed a primitive union with `typeof`.
- [ ] I removed a missing case with an early return.
- [ ] I used `Array.isArray` for an array union.
- [ ] I preserved valid zero or empty values.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
