# Module 15 Exercises

## Exercise 1: Optional profile data

Create a `LearnerProfile` interface with required `name` and optional `bio`. Write `describeProfile` that returns the name and uses `"No bio"` when the bio is missing.

## Exercise 2: Preserve valid zero

Write `getVolume(savedVolume: number | undefined): number`. Return the saved value when present and `50` when missing. Confirm that input `0` returns `0`.

## Exercise 3: Readonly identity

Create a `Course` interface with readonly `id`, writable `title`, and writable `lessonCount`. Create a value, update its title, and try updating its id. Record the error and remove the invalid line.

## Exercise 4: Safe lookup

Create this dictionary type and value:

```typescript
interface PriceLookup {
  [itemName: string]: number;
}

const prices: PriceLookup = {
  pen: 12,
  notebook: 45,
};
```

Write `printPrice(itemName: string): void`. Print a missing message when the lookup returns `undefined`.

## Exercise 5: Compare optional shapes

Create one valid object for each:

```typescript
interface A {
  note?: string;
}

interface B {
  note: string | undefined;
}
```

Explain why `{}` works for one but not the other.

## Completion checklist

- [ ] I handled an optional property.
- [ ] I used `??` without losing zero.
- [ ] I understood the shallow static meaning of `readonly`.
- [ ] I checked a dictionary lookup for `undefined`.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
