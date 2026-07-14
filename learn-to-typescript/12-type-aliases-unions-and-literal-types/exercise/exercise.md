# Module 12 Exercises

## Exercise 1: Model a small set of choices

Create a `TrafficLight` type that permits only `"red"`, `"yellow"`, and `"green"`. Create a variable with that type and assign each valid value.

Try assigning `"blue"`, read the error, then remove the invalid line.

## Exercise 2: String or number identifier

Create a type named `OrderId` that accepts strings or numbers. Write `printOrderId(id: OrderId): void` and print the value in a template string. Call it with both forms.

## Exercise 3: Honest missing result

Write `getDayName(dayNumber: number): string | undefined` for values `1`, `2`, and `3`. Return `"Monday"`, `"Tuesday"`, or `"Wednesday"`. Return `undefined` for any other number.

Store the result for `2`. Use an `if` check to print it only when it is not `undefined`.

## Exercise 4: Choose the precise type

Choose a suitable type for each value and explain your choice:

- a username that can be any text
- a shirt size limited to small, medium, or large
- a selected item that begins with no selection and later contains a string
- a rating from 1 to 5

## Exercise 5: Find an overly broad union

Explain what is unclear about this type, then replace it with a type for a connection state:

```typescript
type Data = string | number | boolean | null;
```

The new state should allow exactly `"offline"`, `"connecting"`, and `"online"`.

## Completion checklist

- [ ] I named a type with `type`.
- [ ] I created string and number literal unions.
- [ ] I modeled a missing result explicitly.
- [ ] I did not treat a type alias as a runtime value.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
