# Module 01: The Basics

This module covers everything you need to understand before writing real TypeScript code. We start from absolute zero. No prior knowledge is assumed.

---

## 1. What is TypeScript?

TypeScript is a programming language built on top of JavaScript. The key difference is that TypeScript forces you to declare what kind of data each variable holds. This allows the editor and compiler to catch mistakes before your program ever runs.

JavaScript is flexible but dangerous
```javascript
// JavaScript allows this, but it crashes at runtime
let age = "twenty five";
age + 10; // Results in "twenty five10", not a number
```

TypeScript stops that mistake immediately
```typescript
// TypeScript catches the wrong type while you are still writing code
let age: number = 25;
// age = "twenty five"; // ERROR! Type 'string' is not assignable to type 'number'.
```

TypeScript is not a separate runtime. It is a development tool. When you are ready to run your code, TypeScript compiles (translates) itself into plain JavaScript.

---

## 2. Variables: `let` and `const`

A variable is a named container that stores a value. You create variables using two keywords
- `let`: Creates a variable whose value can be changed later.
- `const`: Creates a variable whose value can never be reassigned.

```typescript
let score = 10;
score = 20; // Allowed. 'let' variables can change.

const playerName = "Alice";
// playerName = "Bob"; // ERROR! 'const' variables cannot be reassigned.
```

Which one should you use? Use `const` by default. Only use `let` when you know the value needs to change (like a running total or a loop counter).

---

## 3. Primitive Types: `string`, `number`, `boolean`

Every value in TypeScript has a type. A type is a label that tells TypeScript what kind of data is inside a variable. The three most basic types are
- `string`: Any text. Must be wrapped in single quotes, double quotes, or backticks.
- `number`: Any numeric value, including decimals. TypeScript has only one number type (not separate integer/float types).
- `boolean`: Either `true` or `false`. Nothing else.

To explicitly tell TypeScript what type a variable holds, write a colon after the variable name, then the type, then assign the value
```typescript
let username: string = "cool_gamer_99";
let age: number = 25;
let isOnline: boolean = true;
let price: number = 9.99;
```

### Type Inference

TypeScript is smart enough to figure out the type on its own when you assign a value immediately. You do not have to write the type annotation manually in most cases
```typescript
let city = "Tokyo"; // TypeScript infers this is a 'string' automatically.
let score = 100;    // TypeScript infers this is a 'number'.

// Once a type is inferred, it is locked in permanently
// city = 42; // ERROR! Type 'number' is not assignable to type 'string'.
```

---

## 4. `if` Statements and Comparisons

Programs need to make decisions. An `if` statement runs a block of code only when a condition is true.

The condition goes inside parentheses `(...)`. The code to run goes inside curly braces `{ ... }`.

```typescript
let temperature = 35;

if (temperature > 30) {
  console.log("It is hot outside.");
}
```

### Comparison Operators

- `===` (triple equals): Checks if two values are exactly equal. This is different from a single `=`, which assigns a value to a variable.
- `!==`: Checks if two values are NOT equal.
- `>`, `<`, `>=`, `<=`: Greater than, less than, etc.

```typescript
let status = "active";

if (status === "active") {
  console.log("User is active."); // This runs because the condition is true.
}

if (status !== "banned") {
  console.log("User is not banned."); // This also runs.
}
```

### `else` and `else if`

You can chain decisions with `else if` (check another condition if the first was false) and `else` (run code if every condition above was false)
```typescript
let score = 75;

if (score >= 90) {
  console.log("Grade: A");
} else if (score >= 70) {
  console.log("Grade: B"); // This one runs.
} else {
  console.log("Grade: F");
}
```

---

## 5. The `typeof` Operator

`typeof` is a built-in JavaScript operator that inspects a variable at runtime and returns its data type as a plain text string. The possible results are: `"string"`, `"number"`, `"boolean"`, `"undefined"`, `"object"`, and `"function"`.

You use it with an `if` statement to check a variable's type before performing actions specific to that type
```typescript
let value = "Hello";
console.log(typeof value); // Outputs: "string"

let count = 42;
console.log(typeof count); // Outputs: "number"

// Using typeof inside an if-statement to decide what to do
if (typeof value === "string") {
  console.log("It is a string, so we can work with it as text.");
}
```

This becomes very important when a variable could be one of several types, which you will see in later modules.

---

## 6. Built-in Methods for Strings and Numbers

Values in TypeScript come with built-in actions called **methods**. You call a method by writing a dot `.` after the variable name, then the method name, then parentheses `()`.

### String Methods

**`.toUpperCase()`** converts every character in a string to capital letters
```typescript
let greeting = "hello world";
let loud = greeting.toUpperCase();
console.log(loud); // Outputs: "HELLO WORLD"
```

**`.toLowerCase()`** converts every character to lowercase
```typescript
let name = "ALICE";
console.log(name.toLowerCase()); // Outputs: "alice"
```

**`.split(separator)`** chops a string into an array of smaller strings wherever it finds the separator character you provide
```typescript
let sentence = "apple,banana,orange";
let fruits = sentence.split(","); // Chops at every comma.
// Result: ["apple", "banana", "orange"]

let words = "Learn TypeScript".split(" "); // Chops at every space.
// Result: ["Learn", "TypeScript"]
```

**`.trim()`** removes extra whitespace (spaces, tabs) from the beginning and end of a string
```typescript
let messy = "   hello   ";
console.log(messy.trim()); // Outputs: "hello"
```

### Number Methods and Global Functions

**`.toFixed(digits)`** formats a number to have a specific number of decimal places. Note: the result is returned as a string, not a number
```typescript
let price = 9.12345;
console.log(price.toFixed(2)); // Outputs: "9.12"
```

**`parseInt(text)`** converts a string that looks like a whole number into an actual `number`
```typescript
let strNum = "42";
let actualNum = parseInt(strNum); // Result: 42 (as a number)
```

**`parseFloat(text)`** converts a string that looks like a decimal number into an actual `number`
```typescript
let strDecimal = "3.14";
let pi = parseFloat(strDecimal); // Result: 3.14 (as a number)
```

---

## 7. Arrays: Storing Lists of Data

An array is an ordered list of values. You create one using square brackets `[]` with values separated by commas.

To type an array, write the type of data it holds followed by `[]`
```typescript
let friends: string[] = ["Alice", "Bob", "Charlie"];
let scores: number[] = [95, 82, 100];
let flags: boolean[] = [true, false, true];
```

### Accessing Items by Index

Every item in an array has a numbered position called an **index**, starting at `0` for the first item
```typescript
let colors: string[] = ["Red", "Green", "Blue"];

console.log(colors[0]); // "Red"   (first item)
console.log(colors[1]); // "Green" (second item)
console.log(colors[2]); // "Blue"  (third item)
```

### Array Methods

**`.push(value)`** adds a new item to the end of an array. TypeScript will give an error if you try to push the wrong type
```typescript
let names: string[] = ["Alice", "Bob"];
names.push("Charlie"); // Array is now: ["Alice", "Bob", "Charlie"]
// names.push(42); // ERROR! Type 'number' is not assignable to type 'string'.
```

**`.length`** is a property (not a method, so no parentheses) that tells you how many items are in the array
```typescript
let items = ["sword", "shield", "potion"];
console.log(items.length); // Outputs: 3
```

### Why `.push()` works on a `const` array

Using `const` for an array prevents you from replacing the entire array with a new one. But it does NOT prevent you from modifying the contents of that existing array. This is because `const` protects the variable reference (the label pointing to the array in memory), not the contents the array holds.

```typescript
const inventory = ["Sword", "Shield"];
inventory.push("Potion"); // Allowed! Modifying the contents.
// inventory = ["Bow"]; // ERROR! Cannot reassign the variable itself.
```

---

## 8. The `any` Type and the `unknown` Type

### `any` (Avoid It)

Typing a variable as `any` tells TypeScript to completely stop checking it. This defeats the entire purpose of TypeScript. Avoid it unless you have a very specific reason
```typescript
let box: any = "Hello";
box = 42;        // Allowed.
box = true;      // Allowed.
box.fly();       // TypeScript allows this, but it CRASHES at runtime because numbers cannot fly
```

### `unknown` (The Safe Alternative)

`unknown` is the correct way to handle a value whose type you do not know yet. TypeScript will refuse to let you call any methods or access any properties on an `unknown` variable until you first check its type with `typeof`
```typescript
let userInput: unknown = "Hello World";

// This is blocked
// userInput.toUpperCase(); // ERROR! Object is of type 'unknown'.

// You must verify the type first
if (typeof userInput === "string") {
  // Inside this block, TypeScript knows for certain it is a string.
  console.log(userInput.toUpperCase()); // Safe
}
```

---

## 9. Template Literals (Backtick Strings)

Instead of joining strings together with `+`, TypeScript (and JavaScript) supports **template literals**. You wrap the text in backtick characters `` ` `` and embed variable values inside `${ }`
```typescript
let name = "Alice";
let score = 95;

// Old way
let message1 = "Player " + name + " scored " + score + " points.";

// Template literal (much cleaner)
let message2 = `Player ${name} scored ${score} points.`;

console.log(message2); // Outputs: "Player Alice scored 95 points."
```

---

## 10. `console.log`: Printing Output

`console.log(...)` is how you print values to the terminal so you can see what is happening in your program. You can pass any value or multiple values separated by commas
```typescript
let x = 10;
console.log(x);             // Outputs: 10
console.log("x is:", x);   // Outputs: x is: 10
console.log(1, 2, 3);      // Outputs: 1 2 3
```

---

## 11. The TypeScript Compiler (`tsc`)

Computers and browsers only understand JavaScript, not TypeScript. TypeScript is purely a development-time tool for catching errors while you write code.

When you are ready to run your code, you use the TypeScript Compiler (`tsc`), which translates your `.ts` files into `.js` files. During this translation, all type annotations (`: string`, `: number`, `unknown`, etc.) are completely stripped out. Only the raw JavaScript logic remains in the output.

This means TypeScript provides zero runtime overhead. All the safety it provides happens before the code ever runs.
