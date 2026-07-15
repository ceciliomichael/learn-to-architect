# Module 13: JSON Boundaries and Runtime Validation

## What you will learn

Convert unknown decoded data into a trusted application value only after checking its complete required shape.

## Contracts to understand

- Only valid JSON syntax and resulting JavaScript shapes, not application validity.
- Runtime data does not become trustworthy because TypeScript is told a type.
- The domain uses exact integer minor units within reliable JavaScript integer range.
- No, when the domain requires a meaningful name; check after normalization.
- At the boundary before untrusted values enter trusted application behavior.

## Complete TypeScript example

```ts
type Product = {
  readonly id: string;
  readonly name: string;
  readonly priceCents: number;
};

function parseProduct(value: unknown): Product {
  if (typeof value !== "object" || value === null) {
    throw new Error("Product must be an object");
  }

  const record = value as Record<string, unknown>;
  if (
    typeof record.id !== "string" ||
    typeof record.name !== "string" ||
    !Number.isSafeInteger(record.priceCents) ||
    (record.priceCents as number) < 0
  ) {
    throw new Error("Invalid product");
  }

  return {
    id: record.id,
    name: record.name.trim(),
    priceCents: record.priceCents as number,
  };
}
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 14](../14-local-storage-session-storage-and-data-lifetimes/README.md).

