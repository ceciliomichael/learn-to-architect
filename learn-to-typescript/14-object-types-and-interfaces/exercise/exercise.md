# Module 14 Exercises

## Exercise 1: Reuse a book shape

Create a `Book` type alias with `title: string`, `author: string`, and `pages: number`.

Write:

- `describeBook(book: Book): string`
- `isLongBook(book: Book): boolean`, using 300 pages as the boundary

Test both functions with two books.

## Exercise 2: Create an interface

Create a `Task` interface with `title: string` and `isComplete: boolean`. Create an array of tasks and write a function that counts completed tasks.

## Exercise 3: Use a focused contract

Create an interface named `HasName` with only `name: string`. Write `welcome(value: HasName): string`.

Call it with:

```typescript
const student = { name: "Jo", level: 2 };
const teacher = { name: "Rae", subject: "Math" };
```

Explain why both calls work.

## Exercise 4: Find an excess property mistake

Correct this object:

```typescript
interface Product {
  name: string;
  price: number;
}

const product: Product = {
  name: "Pencil",
  pirce: 10,
};
```

## Exercise 5: Choose interface or alias

Choose a valid form for each and explain whether the other form could also work:

- an object shape for `User`
- a union `"draft" | "published"`
- an object shape for `Coordinates`

## Completion checklist

- [ ] I named and reused an object shape.
- [ ] I wrote both an interface and a type alias.
- [ ] I passed structurally compatible values.
- [ ] I kept a function input contract focused.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
