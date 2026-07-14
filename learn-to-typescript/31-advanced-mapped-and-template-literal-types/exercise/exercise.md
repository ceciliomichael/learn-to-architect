# Module 31 Exercises

## Exercise 1: Remove modifiers

Write `Editable<T>` that removes readonly and optional modifiers from every top-level property.

## Exercise 2: Generate commands

From `type Action = "save" | "load" | "reset"`, create `Command = "run-save" | "run-load" | "run-reset"` with a template literal type.

## Exercise 3: Create setters

Write `Setters<T>` that turns each string key into `setKey` with a function accepting the original value type.

## Exercise 4: Filter functions

Write a mapped type that keeps only properties whose values are functions. Use key remapping and a conditional.

## Exercise 5: Explain runtime work

Explain what a class or object must still do after its type is declared as `Getters<Person>`.

## Completion checklist

- [ ] I changed mapped modifiers.
- [ ] I generated a controlled string union.
- [ ] I remapped keys.
- [ ] I kept static generation separate from runtime implementation.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
