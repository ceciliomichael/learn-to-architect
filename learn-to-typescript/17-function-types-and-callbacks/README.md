# Module 17: Function Types and Callbacks

## Before you start

Complete Modules 01 to 16. You should understand functions, array callbacks, aliases, and object types.

## What you will learn

- store and pass functions as values
- write a function type expression
- name callback contracts
- use optional and default parameters accurately
- understand arrow functions and contextual typing
- design callbacks around the information they need

## Why this matters

A callback lets one piece of code decide when work happens while another piece decides what the work is. Clear function types make that agreement visible.

## 1. Functions are values

```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}

const createGreeting = greet;
console.log(createGreeting("Ana"));
```

The function is assigned without calling it. `greet` refers to the function value. `greet("Ana")` calls it and produces a string.

## 2. Function type expressions

```typescript
type StringFormatter = (value: string) => string;

const makeUppercase: StringFormatter = (value) => {
  return value.toUpperCase();
};
```

Read the type from left to right: a function that accepts a string named `value` and returns a string.

Parameter names in a function type document meaning. Compatibility mainly depends on parameter and return types, not matching those parameter names.

## 3. Accept a callback

```typescript
type NumberOperation = (value: number) => number;

function applyOperation(value: number, operation: NumberOperation): number {
  return operation(value);
}

const doubled = applyOperation(4, (value) => value * 2);
const squared = applyOperation(4, (value) => value * value);

console.log(doubled);
console.log(squared);
```

`applyOperation` controls when the callback runs. The caller supplies the calculation.

## 4. Contextual typing in callbacks

In the calls above, TypeScript knows `value` is a number because `operation` expects `NumberOperation`.

This is also valid:

```typescript
const double: NumberOperation = (value) => value * 2;
```

The variable annotation supplies the callback context.

Do not repeat a callback parameter annotation when the context is already clear, unless it improves reading or solves an inference problem.

## 5. Optional parameters

```typescript
function createGreeting(name: string, title?: string): string {
  if (title === undefined) {
    return `Hello, ${name}`;
  }

  return `Hello, ${title} ${name}`;
}
```

An optional parameter may be omitted, so its value inside the function includes `undefined`.

Required parameters cannot follow optional parameters:

```typescript
// Intentional error: a required parameter follows an optional one.
function invalid(first?: string, second: string): void {}
```

## 6. Default parameters

```typescript
function repeatText(text: string, times = 2): string {
  return text.repeat(times);
}

console.log(repeatText("ha"));
console.log(repeatText("ha", 3));
```

The default value gives TypeScript enough information to infer `times` as a number. Callers may omit it or pass `undefined` to use the default.

Inside the function, `times` is a number because the default replaces an undefined argument.

## 7. Arrow functions

These functions have similar behavior in this simple case:

```typescript
function addOne(value: number): number {
  return value + 1;
}

const addOneArrow = (value: number): number => {
  return value + 1;
};
```

An expression body returns automatically:

```typescript
const addOneShort = (value: number): number => value + 1;
```

Arrow functions and standard functions differ in their handling of `this` and in when their declarations are available. Module 29 covers those differences where they matter. Do not choose one because it is always more modern or always better.

## 8. A callback should receive what it needs

```typescript
interface Task {
  title: string;
  isComplete: boolean;
}

type TaskTest = (task: Task) => boolean;

function countMatching(tasks: readonly Task[], test: TaskTest): number {
  let count = 0;

  for (const task of tasks) {
    if (test(task)) {
      count = count + 1;
    }
  }

  return count;
}
```

The callback receives a task because that is the information required to decide. Avoid passing unrelated details.

## 9. Callbacks returning `void`

```typescript
type Reporter = (message: string) => void;

function runWithReport(report: Reporter): void {
  report("Starting");
  report("Finished");
}
```

Here `void` means the caller does not use a returned value from the callback. A provided function may technically return something, but `runWithReport` will ignore it.

## Common mistakes

### Calling a function when you meant to pass it

Pass `greet`, not `greet()`, when the receiver expects a callback and will supply arguments later.

### Forgetting the return type in a function type

`(value: number) => number` includes both input and output.

### Making a parameter optional because the caller currently omits it

Only make it optional when the function can work correctly without it.

### Assuming arrows are always better

Choose based on behavior and readability.

## Check your understanding

1. What is the difference between `greet` and `greet()`?
2. How do you read `(value: number) => string`?
3. Where does a contextually typed callback parameter get its type?
4. What type does an optional parameter include inside a function?
5. What does `void` say about how the caller uses a callback result?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 18](../18-modules-and-code-organization/README.md) splits values and types across files.
