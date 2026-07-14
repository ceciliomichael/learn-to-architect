# Module 25 Exercises

## Exercise 1: Timer class

Create a `Timer` class with a readonly id, private seconds value, `tick()` method, and `getSeconds()` method. Create two independent instances.

## Exercise 2: Implement a contract

Create `interface Formatter { format(text: string): string }`. Implement it with `UppercaseFormatter` and `TrimFormatter` classes.

## Exercise 3: Inheritance

Create a `Message` base class with text and a `describe` method. Extend it with `TimedMessage` that adds a timestamp and overrides `describe`. Use `super` correctly.

## Exercise 4: Composition

Create a `Notifier` interface. Build an `OrderService` that receives a Notifier in its constructor and calls it after completing an order. Provide a console notifier implementation.

## Exercise 5: Custom validation error

Create a `ValidationError` with readonly field name. Throw it for an empty username and catch it with `instanceof`.

## Completion checklist

- [ ] I created separate class instances.
- [ ] I protected a field and exposed behavior.
- [ ] I implemented an interface.
- [ ] I compared inheritance with composition.
- [ ] I used a custom error only for structured meaning.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
