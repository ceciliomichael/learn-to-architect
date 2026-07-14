# Module 14: Object Types and Interfaces

## Before you start

Complete Modules 01 to 13. You should understand objects, aliases, unions, and narrowing.

## What you will learn

- describe an object shape inline
- reuse object shapes with type aliases and interfaces
- understand structural compatibility
- decide between an interface and a type alias without invented rules
- keep object contracts focused on what code needs

## Why this matters

Objects carry related data through a program. A named object type tells readers which properties are required and lets many functions agree on the same shape.

## 1. Inline object types

You have seen a function like this:

```typescript
function printBook(book: { title: string; pages: number }): void {
  console.log(`${book.title}: ${book.pages} pages`);
}
```

The inline type is clear when used once and kept short.

If several functions need the same shape, repeating it can drift:

```typescript
function printBook(book: { title: string; pages: number }): void {}
function isLongBook(book: { title: string; pages: number }): boolean {
  return book.pages > 300;
}
```

Give the shape a name.

## 2. Object shape with a type alias

```typescript
type Book = {
  title: string;
  pages: number;
};

function printBook(book: Book): void {
  console.log(`${book.title}: ${book.pages} pages`);
}

function isLongBook(book: Book): boolean {
  return book.pages > 300;
}
```

Object type members commonly use semicolons. Object values use commas. TypeScript accepts some variations, but this distinction keeps course examples consistent.

## 3. Object shape with an interface

```typescript
interface Book {
  title: string;
  pages: number;
}
```

For this ordinary object shape, the interface behaves like the alias shown above.

Create a matching value:

```typescript
const book: Book = {
  title: "A Wizard of Earthsea",
  pages: 205,
};
```

Missing or mismatched required properties cause errors.

## 4. Methods in object types

An object can include function properties:

```typescript
interface Counter {
  value: number;
  increment(): void;
}

const counter: Counter = {
  value: 0,
  increment() {
    this.value = this.value + 1;
  },
};
```

`increment(): void` describes a method with no parameters and no useful returned value.

Use method syntax when the action naturally belongs to the object. Plain functions are often simpler when no object state is needed.

## 5. Structural typing

TypeScript checks whether a value has the required structure:

```typescript
interface Named {
  name: string;
}

const person = {
  name: "Mina",
  age: 24,
};

function printName(value: Named): void {
  console.log(value.name);
}

printName(person);
```

This works because `person` has at least the required `name: string` property. It did not need to declare that it implements `Named`.

Structural compatibility is based on available members, not only a declared type name.

## 6. Excess property checking

This direct object literal gets an extra check:

```typescript
interface Profile {
  name: string;
}

// Intentional error: agge is probably a misspelling.
const profile: Profile = {
  name: "Mina",
  agge: 24,
};
```

The extra check helps catch mistakes in fresh object literals.

A previously stored value can have extra properties and still satisfy a smaller required shape:

```typescript
const detailedProfile = { name: "Mina", age: 24 };
const simpleProfile: Profile = detailedProfile;
```

This is not a loophole for ignoring errors. It reflects structural typing: code using `Profile` promises to rely only on `name`.

## 7. Interface or type alias

Both can name an object shape. Choose a consistent local style unless a real difference matters.

Use a type alias when you need to name:

- a union
- a primitive alias
- a tuple
- a type expression produced by other type tools

An interface is only for object-like shapes and can be reopened by another declaration with the same name. That behavior is valuable for some library extension patterns but can be surprising in application code.

Neither choice makes runtime code faster. Both are erased as type information.

There is no universal rule that every domain object must use one form.

## 8. Keep contracts focused

If a function needs only a title, it can ask for only a title:

```typescript
type Titled = {
  title: string;
};

function printTitle(item: Titled): void {
  console.log(item.title);
}
```

A smaller input contract makes the function usable with books, tasks, articles, and other titled objects.

Do not include properties a function does not use merely because one current caller has them.

## Common mistakes

### Adding an equals sign to an interface

Write `interface Book { title: string }`, not `interface Book = { title: string }`.

### Treating a named type as runtime validation

It checks known source code. External data still needs runtime validation.

### Requiring a large object when a function uses one property

Describe the minimum honest contract.

### Debating interface versus alias as if one is always correct

Use the actual language differences and team consistency to decide.

## Check your understanding

1. When is an inline object type reasonable?
2. How do a type alias and interface overlap for ordinary object shapes?
3. What does structural typing compare?
4. Why are fresh object literals checked for extra properties?
5. Does either object type syntax validate network data at runtime?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 15](../15-optional-and-readonly-data/README.md) models properties that may be missing or should not be assigned through a type.
