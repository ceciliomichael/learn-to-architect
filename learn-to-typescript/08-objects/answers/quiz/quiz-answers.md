# Module 08 Quiz Answers

## Answer 1

- `name` has a string value.
- `price` has a number value.
- `inStock` has a boolean value.

## Answer 2

No. It prevents reassignment of the variable to a different object. Writable properties of the existing object can still change.

## Answer 3

```text
5
```

Both variables refer to the same object, so the change through `second` is visible through `first`.

## Answer 4

Assignment gives the same object another name. Object spread creates a new outer object and copies the property values. For primitive properties, later updates to one outer object do not update the other. Spread is still only a shallow copy when values contain nested objects.

## Answer 5

```typescript
const user = { name: "Kai", age: 20 };
console.log(user.name);
```

An object literal uses a colon between a property name and value. Property names are case-sensitive.
