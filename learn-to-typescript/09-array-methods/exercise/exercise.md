# Module 09 Exercises

Use this data for the exercises:

```typescript
const books = [
  { title: "Dune", pages: 412, isRead: true },
  { title: "Coraline", pages: 176, isRead: false },
  { title: "Matilda", pages: 240, isRead: true },
  { title: "The Hobbit", pages: 310, isRead: false },
];
```

## Warm-up: Print titles

Use `forEach` to print every title.

## Guided exercise: Create labels

Use `map` to create this new array:

```text
["Dune: 412 pages", "Coraline: 176 pages", "Matilda: 240 pages", "The Hobbit: 310 pages"]
```

Store the result in `bookLabels` and print it.

## Independent exercise: Unread long books

Use `filter` to create an array containing books that are unread and have at least 300 pages. Print the result.

## Search exercise

1. Use `find` to get the book titled `"Matilda"`.
2. Check that a book was found before printing its page count.
3. Use `some` to check whether any book has more than 400 pages.
4. Use `every` to check whether every book has at least 100 pages.

## Debugging task

Fix this code so it creates `[2, 4, 6]`:

```typescript
const numbers = [1, 2, 3];

const doubled = numbers.forEach((number) => {
  number * 2;
});

console.log(doubled);
```

Explain both problems.

## Completion checklist

- [ ] I chose methods based on the result I needed.
- [ ] I stored the new arrays returned by `map` or `filter`.
- [ ] I checked a `find` result before using it.
- [ ] I returned a value from callback blocks that needed one.

Then compare with the [exercise solutions](../answers/exercise/exercise-solutions.md).
