# Module 20 Exercises

## Exercise 1: Narrow a primitive

Write `formatUnknown(value: unknown): string`. Return uppercase text for a string, a two-decimal string for a number, and `"Unsupported value"` for everything else.

## Exercise 2: Validate settings

Create:

```typescript
interface Settings {
  theme: "light" | "dark";
  fontSize: number;
}
```

Write `isSettings(value: unknown): value is Settings`. Validate that the value is a non-null, non-array object, the theme is one of the two exact strings, and font size is a number.

## Exercise 3: Validate an array

Write `isNumberArray(value: unknown): value is number[]`. Test a number array, a mixed array, and a non-array.

## Exercise 4: Parse a value

Parse these strings into variables typed as `unknown`, then validate them:

```typescript
const validJson = '{"theme":"dark","fontSize":16}';
const invalidJson = '{"theme":"blue","fontSize":"large"}';
```

Do not use an assertion.

## Exercise 5: Explain the unsafe claim

Explain why this can fail even though the file type-checks:

```typescript
const settings = JSON.parse('{"theme":42}') as Settings;
console.log(settings.theme.toUpperCase());
```

## Completion checklist

- [ ] I accepted uncertain input as `unknown`.
- [ ] I checked object and property types at runtime.
- [ ] I validated every array item.
- [ ] I did not use an assertion as validation.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
