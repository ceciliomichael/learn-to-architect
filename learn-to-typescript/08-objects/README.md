# Module 08: Objects

## Before you start

Complete Modules 01 to 07. You should be able to write functions and work with arrays.

## What you will learn

- group related values in an object
- read and update properties
- use bracket access with a known property name
- pass objects to functions
- understand references and shallow copies

## Why this matters

An array stores a list of similar items. An object groups facts that belong to one thing, such as a book's title, page count, and availability.

## 1. Create an object literal

```typescript
const book = {
  title: "The Hobbit",
  pageCount: 310,
  isAvailable: true,
};
```

The braces create an object. Each property has a name, a colon, and a value. Commas separate properties.

TypeScript infers this shape:

- `title` is a string
- `pageCount` is a number
- `isAvailable` is a boolean

You will learn how to name object shapes in Module 14.

## 2. Read properties with dot access

```typescript
console.log(book.title);
console.log(book.pageCount);
console.log(book.isAvailable);
```

Dot access is the clearest choice when the property name is known while writing the code.

TypeScript catches misspellings:

```typescript
// Intentional error: the property is named title.
console.log(book.titel);
```

## 3. Update a property

```typescript
const task = {
  title: "Read Module 08",
  isComplete: false,
};

task.isComplete = true;
console.log(task.isComplete);
```

The `const` name still refers to the same object. A property inside that object can change.

TypeScript keeps the property type consistent:

```typescript
// Intentional error: isComplete is a boolean property.
task.isComplete = "yes";
```

## 4. Bracket access

This is another way to read a known property:

```typescript
console.log(book["title"]);
```

Bracket access becomes important when a property name comes from another value. Safe dynamic keys need additional type ideas, so Module 23 covers them fully.

For ordinary known names, prefer `book.title`.

## 5. Pass an object to a function

An inline object type describes the properties a parameter needs:

```typescript
function printBookSummary(book: { title: string; pageCount: number }) {
  console.log(`${book.title} has ${book.pageCount} pages.`);
}

printBookSummary({
  title: "Charlotte's Web",
  pageCount: 192,
});
```

The parameter requires both properties with the stated types. Module 14 shows how to give this shape a reusable name.

## 6. Arrays of objects

```typescript
const products = [
  { name: "Pencil", price: 10 },
  { name: "Notebook", price: 45 },
];

for (const product of products) {
  console.log(`${product.name}: ${product.price} pesos`);
}
```

Each array item is an object with the same inferred shape.

## 7. Objects are reference values

This code creates two names for the same object:

```typescript
const original = { count: 1 };
const anotherName = original;

anotherName.count = 2;

console.log(original.count);
```

The output is `2`. No object was copied. Both variables refer to the same object.

Create a shallow copy with object spread:

```typescript
const originalTask = { title: "Study", isComplete: false };
const copiedTask = { ...originalTask };

copiedTask.isComplete = true;

console.log(originalTask.isComplete);
console.log(copiedTask.isComplete);
```

The spread creates a new outer object. Nested objects are still shared by a shallow copy.

## 8. Add a property by creating a new object

TypeScript infers the exact known shape of an object variable. This causes an error:

```typescript
const person = { name: "Ira" };

// Intentional error: age is not part of the inferred shape.
person.age = 24;
```

Create the full shape from the beginning or create a new object:

```typescript
const personWithAge = {
  ...person,
  age: 24,
};
```

## Predict the result

```typescript
const first = { value: 5 };
const second = first;
const third = { ...first };

second.value = 8;
third.value = 10;

console.log(first.value);
console.log(second.value);
console.log(third.value);
```

## Common mistakes

### Using `=` instead of `:` inside an object literal

Write `name: "Ari"` inside an object.

### Treating a `const` object as frozen

The variable cannot be reassigned, but its writable properties can change.

### Assuming assignment copies an object

`const b = a` gives the same object another name.

### Adding a property TypeScript did not infer

Create the intended shape from the beginning or define a suitable object type later.

## Check your understanding

1. What does an object group together?
2. When is dot access a clear choice?
3. Does `const` freeze an object's properties?
4. What happens when one object variable is assigned to another?
5. What kind of copy does object spread create?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 09](../09-array-methods/README.md) combines arrays, objects, functions, and short callbacks.
