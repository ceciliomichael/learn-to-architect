# Module 14 Exercise Solutions

## Exercise 1

```typescript
type Book = {
  title: string;
  author: string;
  pages: number;
};

function describeBook(book: Book): string {
  return `${book.title} by ${book.author}`;
}

function isLongBook(book: Book): boolean {
  return book.pages >= 300;
}

const shortBook: Book = { title: "Coraline", author: "Neil Gaiman", pages: 176 };
const longBook: Book = { title: "Dune", author: "Frank Herbert", pages: 412 };

console.log(describeBook(shortBook));
console.log(isLongBook(shortBook));
console.log(isLongBook(longBook));
```

## Exercise 2

```typescript
interface Task {
  title: string;
  isComplete: boolean;
}

function countCompleted(tasks: Task[]): number {
  let count = 0;

  for (const task of tasks) {
    if (task.isComplete) {
      count = count + 1;
    }
  }

  return count;
}

const tasks: Task[] = [
  { title: "Read", isComplete: true },
  { title: "Practice", isComplete: false },
];

console.log(countCompleted(tasks));
```

## Exercise 3

```typescript
interface HasName {
  name: string;
}

function welcome(value: HasName): string {
  return `Welcome, ${value.name}`;
}

const student = { name: "Jo", level: 2 };
const teacher = { name: "Rae", subject: "Math" };

console.log(welcome(student));
console.log(welcome(teacher));
```

Both objects have the required `name: string` structure. Extra properties do not stop previously stored values from satisfying the smaller contract.

## Exercise 4

```typescript
interface Product {
  name: string;
  price: number;
}

const product: Product = {
  name: "Pencil",
  price: 10,
};
```

The misspelled property was not the required `price` property.

## Exercise 5

```typescript
interface User {
  name: string;
}

type PublicationStatus = "draft" | "published";

type Coordinates = {
  x: number;
  y: number;
};
```

`User` and `Coordinates` could each use either an interface or an object type alias. The union requires a type alias because an interface cannot directly name a union.
