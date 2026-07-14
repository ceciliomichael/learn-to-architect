# Module 17 Exercises

## Exercise 1: Describe a transformer

Create `type TextTransformer = (text: string) => string`. Implement lowercase and uppercase transformers. Write `transformText` that accepts text and a transformer.

## Exercise 2: Number test callback

Create `type NumberTest = (value: number) => boolean`. Write `countNumbers` that accepts a readonly number array and a test callback. Count values for which the callback returns true.

Test it with a callback for even numbers and another for numbers greater than 10.

## Exercise 3: Optional versus default

Write:

- `greet(name: string, title?: string): string`
- `multiply(value: number, factor?: number): number`, but use a default value of `2` rather than an optional type annotation

Explain how the parameter values differ inside the functions.

## Exercise 4: Pass, do not call

Fix the callback argument:

```typescript
function announce(message: string): void {
  console.log(message);
}

function run(report: (message: string) => void): void {
  report("Running");
}

run(announce());
```

## Exercise 5: Expression and block arrows

Write one arrow function with an expression body and the same function with a block body. Both should accept a number and return its square.

## Completion checklist

- [ ] I wrote and named a function type.
- [ ] I passed a function without calling it early.
- [ ] I used contextual typing.
- [ ] I distinguished optional and default parameters.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
