# Module 23 Exercises

## Exercise 1: Derive keys

Create a `Product` interface with `id`, `name`, `price`, and `inStock`. Create `ProductKey` with `keyof`. Assign every valid key and try one invalid key.

## Exercise 2: Derive property values

Create aliases for the name type, price type, and the union of all `Product` property value types.

## Exercise 3: Generic getter

Implement `getProperty<T, K extends keyof T>`. Confirm that the name result is a string and price result is a number. Try an invalid key.

## Exercise 4: Derive from defaults

Create a `defaultPreferences` object with string theme, number font size, and boolean reduced motion. Derive `Preferences` with type-position `typeof`, then create another matching value.

## Exercise 5: Explain both `typeof` uses

Explain the output or meaning of each line:

```typescript
console.log(typeof defaultPreferences);
type Preferences = typeof defaultPreferences;
```

## Completion checklist

- [ ] I derived a key union.
- [ ] I looked up a property type.
- [ ] I connected a generic key to its result.
- [ ] I distinguished both uses of `typeof`.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
