# Module 06: Functions

## Before you start

Complete Modules 01 to 05. You should understand variables, decisions, and loops.

## What you will learn

- place reusable steps in a function
- pass information through parameters
- receive a result with `return`
- understand local scope
- keep functions small and focused

## Why this matters

When several parts of a program need the same calculation, copying the code creates extra work. A function gives those steps a name and lets you use them with different values.

## 1. Declare and call a function

```typescript
function printWelcome() {
  console.log("Welcome to the course");
}

printWelcome();
printWelcome();
```

The declaration creates the function. Its body is between the braces. The body does not run until the function is called with `printWelcome()`.

This program calls the function twice, so it prints the message twice.

## 2. Parameters receive information

```typescript
function greet(name: string) {
  console.log(`Hello, ${name}!`);
}

greet("Noah");
greet("Lia");
```

`name` is a parameter. It is a local name available inside the function. `: string` says the function expects text.

`"Noah"` and `"Lia"` are arguments. An argument is the value supplied during a particular call.

TypeScript rejects this call:

```typescript
// Intentional error: greet expects a string.
greet(42);
```

## 3. Return a result

```typescript
function add(left: number, right: number) {
  return left + right;
}

const total = add(4, 6);
console.log(total);
```

`return` sends a value back to the place where the function was called. TypeScript infers that `add` returns a number because it returns `left + right`.

Printing and returning are different:

- `console.log` displays information.
- `return` gives information back to the caller.

A returned value can be stored, compared, or used in another calculation.

## 4. Code after `return` does not run

```typescript
function describeScore(score: number) {
  if (score >= 70) {
    return "Passing";
  }

  return "Keep practicing";
}
```

When the first return runs, the function ends immediately. The final return handles scores below 70.

## 5. Local scope

A variable created inside a function is local to that function:

```typescript
function calculateDouble(value: number) {
  const doubled = value * 2;
  return doubled;
}

console.log(calculateDouble(5));

// Intentional error: doubled is not available here.
console.log(doubled);
```

Local variables help keep one function's work from interfering with another part of the program.

Code inside a function can read a variable from an outer scope, but passing required information as parameters usually makes the function easier to understand and test.

## 6. One clear job

This function has one job:

```typescript
function calculateArea(width: number, height: number) {
  return width * height;
}
```

This separation is useful:

```typescript
const area = calculateArea(5, 3);
console.log(`The area is ${area}.`);
```

The function calculates. The caller decides how to display the result.

A function does not need to be tiny at all costs. It should have one purpose that can be explained in a short sentence.

## 7. Names should describe actions

Function names often begin with an action word:

```typescript
function calculateTotal(price: number, quantity: number) {
  return price * quantity;
}

function isAdult(age: number) {
  return age >= 18;
}

function formatGreeting(name: string) {
  return `Hello, ${name}!`;
}
```

Names such as `doThing` or `process` do not tell a reader enough.

## 8. Functions can call functions

```typescript
function calculateSubtotal(price: number, quantity: number) {
  return price * quantity;
}

function calculateTotal(price: number, quantity: number, delivery: number) {
  const subtotal = calculateSubtotal(price, quantity);
  return subtotal + delivery;
}

console.log(calculateTotal(50, 3, 20));
```

Small functions can be combined into a larger task.

## Predict the result

```typescript
function multiplyByThree(value: number) {
  return value * 3;
}

const first = multiplyByThree(2);
const second = multiplyByThree(first);

console.log(first);
console.log(second);
```

Trace the two calls before running the code.

## Common mistakes

### Declaring a function but not calling it

The body runs only when you use parentheses to call the function.

### Printing instead of returning

Return a value when later code needs to use it.

### Forgetting an argument

TypeScript checks whether the call supplies the required arguments.

### Using a local variable outside its function

Return the needed value instead.

## Check your understanding

1. What is the difference between a parameter and an argument?
2. What does `return` do?
3. Does a function body run when it is declared?
4. Where can a local variable be used?
5. Why can a calculation function be more useful when it returns instead of prints?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 07](../07-arrays/README.md) teaches how to store an ordered list and process its items.
