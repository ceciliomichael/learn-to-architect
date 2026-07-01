# Module 03: Functions and Signatures

Functions are the building blocks of any program. They are reusable blocks of code that take input, perform some logic, and produce an output. This module covers everything about writing and typing functions in TypeScript.

---

## 1. What is a Function?

A function groups a set of instructions under a name so you can run them repeatedly without rewriting code. You define a function once and call it as many times as you need.

```typescript
function sayHello(name: string): void {
  console.log("Hello, " + name);
}

sayHello("Alice"); // Outputs: Hello, Alice
sayHello("Bob");   // Outputs: Hello, Bob
```

Breaking down the syntax:
- `function`: the keyword that declares a function.
- `sayHello`: the name you give it.
- `(name: string)`: the input the function accepts, called a **parameter**. We type it as `string`.
- `: void`: the **return type**. `void` means this function does not return any value.
- `{ ... }`: the body of the function where the logic lives.

---

## 2. Return Types

When a function produces a result and hands it back to the caller, we say it **returns** a value. The `return` keyword sends the value back. The return type goes after the closing parenthesis of the parameters:

```typescript
function addNumbers(a: number, b: number): number {
  return a + b; // Sends the result back to whoever called this function.
}

let result = addNumbers(10, 5); // result is now 15
console.log(result); // Outputs: 15
```

If a function does not return anything (it just performs an action like logging), use `void` as the return type:

```typescript
function logMessage(message: string): void {
  console.log(message); // Does something, but returns nothing.
}
```

---

## 3. Arrow Functions

Arrow functions are a shorter way to write functions. Instead of the `function` keyword, you use the `=>` symbol (read as "arrow"):

```typescript
// Regular function:
function multiply(a: number, b: number): number {
  return a * b;
}

// Same function as an arrow function:
const multiply = (a: number, b: number): number => {
  return a * b;
};

// Even shorter for single-expression functions:
const multiply = (a: number, b: number): number => a * b;
```

Arrow functions are especially common when passing functions as arguments (callbacks), which is covered below.

---

## 4. Optional Parameters and Default Parameters

### Optional Parameters

You can make a parameter optional by adding `?` after its name. Inside the function, you must check whether it was provided before using it:

```typescript
function greet(name: string, title?: string): string {
  if (title !== undefined) {
    return "Hello, " + title + " " + name;
  }
  return "Hello, " + name;
}

greet("Alice");          // "Hello, Alice"
greet("Alice", "Dr.");   // "Hello, Dr. Alice"
```

### Default Parameters

A default parameter provides a fallback value that is used automatically when the caller does not pass that argument:

```typescript
function greet(name: string, title: string = "Explorer"): string {
  return "Hello, " + title + " " + name;
}

greet("Alice");           // "Hello, Explorer Alice" (uses default)
greet("Alice", "Dr.");    // "Hello, Dr. Alice" (uses provided value)
```

---

## 5. Rest Parameters

Sometimes you want a function to accept any number of arguments without knowing in advance how many will be passed. You do this with a **rest parameter**, which collects all the extra arguments into an array. You write it by putting `...` before the parameter name:

```typescript
function sumAll(...numbers: number[]): number {
  let total = 0;
  for (let num of numbers) {
    total = total + num;
  }
  return total;
}

console.log(sumAll(10, 20, 30));       // Outputs: 60
console.log(sumAll(1, 2, 3, 4, 5));   // Outputs: 15
```

The `for...of` loop used above is a simple way to go through every item in an array one by one.

---

## 6. Callback Functions

A **callback** is when you pass a function as an argument to another function. The receiving function will call your function at some point during its execution. This is one of the most common patterns in JavaScript and TypeScript:

```typescript
function runTwice(action: () => void): void {
  action(); // Call the function the first time.
  action(); // Call it again.
}

function sayHi(): void {
  console.log("Hi!");
}

runTwice(sayHi); // Outputs: Hi! (then) Hi!
```

The type `() => void` means: "a function that takes no parameters and returns nothing." If you have a callback that takes parameters:

```typescript
function applyToNumber(n: number, transform: (x: number) => number): number {
  return transform(n);
}

let result = applyToNumber(5, (x) => x * x); // Passes 5 through the squaring function.
console.log(result); // Outputs: 25
```

---

## 7. Array Methods That Use Callbacks

TypeScript arrays have powerful built-in methods that accept callback functions. These are among the most commonly used tools in real projects.

### `.forEach(callback)`

Runs your callback function once for every item in the array. It does not return a new array. Use it when you want to do something with each item (like logging or sending data):

```typescript
let fruits = ["Apple", "Banana", "Orange"];

fruits.forEach((fruit) => {
  console.log("Eating: " + fruit);
});
// Outputs:
// Eating: Apple
// Eating: Banana
// Eating: Orange
```

### `.map(callback)`

Transforms every item in an array and returns a brand new array containing the transformed results. The original array is not changed:

```typescript
let prices = [10, 20, 30];
let discounted = prices.map((price) => price * 0.9);
// discounted is now [9, 18, 27]. The original 'prices' array is unchanged.
```

### `.filter(callback)`

Creates a new array containing only the items for which your callback returns `true`. Items where the callback returns `false` are left out:

```typescript
let scores = [45, 72, 88, 31, 95];
let passing = scores.filter((score) => score >= 60);
// passing is now [72, 88, 95]
```

### Contextual Typing in Array Callbacks

When you pass an arrow function into `.map()`, `.filter()`, or `.forEach()`, TypeScript automatically infers the type of the callback parameter based on the array's type. You do not need to write the type manually:

```typescript
let names: string[] = ["Alice", "Bob"];

// TypeScript already knows 'name' is a string because the array holds strings:
let upper = names.map((name) => name.toUpperCase());
```

---

## 8. The `void` Return Type and Callbacks

When you define a callback type that returns `void`, TypeScript means: "I do not care what this function returns. I will ignore the return value." This is intentional so that callbacks like `forEach` remain compatible with functions that do return values:

```typescript
function runCallback(cb: () => void): void {
  cb();
}

// Even though this arrow function returns 'true', passing it is valid.
// TypeScript simply ignores the return value because the callback type is void:
runCallback(() => true);
```

---

## 9. Function Overloads

Sometimes a function should behave differently depending on the types of arguments passed. TypeScript lets you define **overload signatures**: multiple versions of the function header that describe the different input/output combinations. Below those, you write a single implementation that handles all the cases:

```typescript
// Overload signatures (these define what callers can pass):
function parseInput(value: string): string[];
function parseInput(value: number): string;

// Implementation (handles all the cases internally):
function parseInput(value: string | number): string[] | string {
  if (typeof value === "string") {
    return value.split(","); // Splits "apple,banana" into ["apple", "banana"]
  } else {
    return value.toFixed(2); // Turns 9.1 into "9.10"
  }
}

const result1 = parseInput("apple,banana"); // TypeScript knows this returns string[]
const result2 = parseInput(9.1);            // TypeScript knows this returns string
```

External callers can only use the overload signatures. They cannot call the function with argument types not listed in the overloads.

---

## 10. The `for` Loop and `for...of` Loop

Loops allow you to repeat an action multiple times.

### `for` loop

The classic `for` loop has three parts: a starting counter, a condition to keep going, and an update step after each run:

```typescript
for (let i = 0; i < 3; i++) {
  console.log("Step: " + i);
}
// Outputs: Step: 0, Step: 1, Step: 2
```

### `for...of` loop

The `for...of` loop is simpler. It automatically goes through every item in an array one by one:

```typescript
let items = ["Sword", "Shield", "Potion"];

for (let item of items) {
  console.log(item);
}
// Outputs: Sword, Shield, Potion
```

Use `for...of` when you want every item. Use the classic `for` loop when you need to track the index number.
