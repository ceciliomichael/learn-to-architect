# Module 11 Exercises

## Exercise 1: Mark inferred and annotated types

For each line, write whether the type is inferred or explicitly annotated. Then write the resulting type.

```typescript
const course = "TypeScript";
let lesson: number = 11;
const complete = false;
const scores: number[] = [];
```

## Exercise 2: Remove unnecessary noise

Rewrite this code with fewer annotations while keeping the same type safety:

```typescript
const title: string = "Morning Plan";
const minutes: number = 25;
const isComplete: boolean = false;
const labels: string[] = ["study", "focus"];
```

Explain which annotation you might keep if the array began empty.

## Exercise 3: Protect a function contract

Write `calculateRectangleArea` with number parameter annotations and an explicit number return type. Call it with width `5` and height `4`.

Then intentionally return a template string instead of a number. Read the error, undo the change, and record what the return annotation protected.

## Exercise 4: Observe contextual typing

Create a number array. Use `map` to double every value without annotating the callback parameter. Hover over the parameter in your editor and record the type TypeScript inferred.

## Exercise 5: Compare source and output

Create `source.ts`:

```typescript
function describeCount(count: number): string {
  return `Count: ${count}`;
}

console.log(describeCount(3));
```

Run:

```text
npx tsc source.ts --target es2022
```

Open `source.js`. List the TypeScript syntax that was removed.

## Completion checklist

- [ ] I let obvious local values be inferred.
- [ ] I annotated a function parameter contract.
- [ ] I saw a return annotation catch a mismatch.
- [ ] I inspected emitted JavaScript.

Compare with the [exercise solutions](../answers/exercise/exercise-solutions.md).
