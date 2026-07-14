# Module 09 Exercise Solutions

## Starting data

```typescript
const books = [
  { title: "Dune", pages: 412, isRead: true },
  { title: "Coraline", pages: 176, isRead: false },
  { title: "Matilda", pages: 240, isRead: true },
  { title: "The Hobbit", pages: 310, isRead: false },
];
```

## Warm-up solution

```typescript
books.forEach((book) => {
  console.log(book.title);
});
```

`forEach` suits this task because printing is the desired action. No new array is needed.

## Guided exercise solution

```typescript
const bookLabels = books.map((book) => {
  return `${book.title}: ${book.pages} pages`;
});

console.log(bookLabels);
```

Every input book produces exactly one output string.

## Independent exercise solution

```typescript
const unreadLongBooks = books.filter((book) => {
  return !book.isRead && book.pages >= 300;
});

console.log(unreadLongBooks);
```

Only `The Hobbit` satisfies both conditions.

## Search exercise solution

```typescript
const matilda = books.find((book) => book.title === "Matilda");

if (matilda !== undefined) {
  console.log(matilda.pages);
}

const hasVeryLongBook = books.some((book) => book.pages > 400);
const allHaveAtLeastOneHundredPages = books.every((book) => book.pages >= 100);

console.log(hasVeryLongBook);
console.log(allHaveAtLeastOneHundredPages);
```

Expected output:

```text
240
true
true
```

## Debugging task solution

```typescript
const numbers = [1, 2, 3];

const doubled = numbers.map((number) => {
  return number * 2;
});

console.log(doubled);
```

The original used `forEach`, which returns `undefined`. The task needs `map`, which creates a new array. The callback also had braces but did not return the calculated value.

A valid shorter version is:

```typescript
const doubled = numbers.map((number) => number * 2);
```
