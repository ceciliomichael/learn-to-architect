# Module 18 Exercise Solutions

## Exercise 1

```typescript
// src/math.ts
export function add(left: number, right: number): number {
  return left + right;
}

export function multiply(left: number, right: number): number {
  return left * right;
}
```

```typescript
// src/index.ts
import { add, multiply } from "./math.js";

console.log(add(2, 3));
console.log(multiply(2, 3));
```

## Exercise 2

```typescript
// src/book.ts
export interface Book {
  title: string;
  author: string;
}

function normalizeTitle(title: string): string {
  return title.trim();
}

export function describeBook(book: Book): string {
  return `${normalizeTitle(book.title)} by ${book.author}`;
}
```

```typescript
// src/index.ts
import { describeBook } from "./book.js";
import type { Book } from "./book.js";

const book: Book = {
  title: " Dune ",
  author: "Frank Herbert",
};

console.log(describeBook(book));
```

`normalizeTitle` is an implementation detail, so it remains unexported.

## Exercise 3

```typescript
import { calculateTotal as getTotal } from "./totals.js";

console.log(getTotal(50, 3));
```

The exported name remains `calculateTotal`. Only this importing module uses the local alias.

## Exercise 4

```typescript
// names.ts
export function formatName(name: string): string {
  return name.trim().toUpperCase();
}
```

The original function was private to its module because it had no export.

## Exercise 5

One reasonable answer is:

```text
src/
  index.ts
  book.ts
  reading-list.ts
```

- `book.ts` defines book data and single-book operations.
- `reading-list.ts` contains operations on a collection of books.
- `index.ts` creates the data and coordinates output.

Other layouts are valid when each boundary has a clear reason.
