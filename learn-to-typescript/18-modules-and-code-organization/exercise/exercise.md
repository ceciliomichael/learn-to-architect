# Module 18 Exercises

Use a new folder or your existing practice project. Run the files with `npx tsx src/index.ts`.

## Exercise 1: Split a calculation

Create `src/math.ts` with named exports `add` and `multiply`. Create `src/index.ts`, import both functions from `"./math.js"`, call them, and print the results.

## Exercise 2: Split a value and type

Create `src/book.ts` with:

- an exported `Book` interface
- an exported `describeBook(book: Book): string` function
- one unexported helper used only by `describeBook`

In `src/index.ts`, import the function normally and the interface with `import type`. Create a book and print its description.

## Exercise 3: Rename an import

Export `calculateTotal` from a module. Import it locally as `getTotal` and call it.

## Exercise 4: Repair module visibility

Why can `main.ts` not import `formatName` here? Fix it.

```typescript
// names.ts
function formatName(name: string): string {
  return name.trim().toUpperCase();
}
```

```typescript
// main.ts
import { formatName } from "./names.js";
```

## Exercise 5: Explain a file boundary

For a simple reading list, propose three or fewer source files. Write one sentence describing the responsibility of each file. Do not add a file without a clear responsibility.

## Completion checklist

- [ ] I used named exports and imports.
- [ ] I kept an internal helper unexported.
- [ ] I used `import type` for a type-only name.
- [ ] My relative paths matched the Node ESM runtime plan.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
