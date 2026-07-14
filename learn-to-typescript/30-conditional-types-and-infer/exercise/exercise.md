# Module 30 Exercises

## Exercise 1: Simple choice

Write `PrimitiveName<T>` that produces `"text"` for strings and `"other"` for other types.

## Exercise 2: Observe distribution

Write `BoxEach<T> = T extends unknown ? { value: T } : never`. Apply it to `string | number` and explain the result.

## Exercise 3: Keep numbers

Write a distributive conditional that filters a union to numeric members.

## Exercise 4: Infer an item

Write `ArrayItem<T>` for mutable and readonly arrays. Test it with `readonly string[]` and a non-array.

## Exercise 5: Infer a property

Write `IdType<T>` that returns the type of an `id` property or `never`.

## Completion checklist

- [ ] I wrote a conditional type.
- [ ] I observed distribution over a union.
- [ ] I used `never` to filter members.
- [ ] I captured a type with `infer`.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
