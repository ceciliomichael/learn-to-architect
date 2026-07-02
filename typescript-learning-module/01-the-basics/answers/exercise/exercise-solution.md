# Module 01 Exercise Solutions

Here are the complete solutions and explanations for the Module 01 exercises.

---

### Solution 1: The Buggy Profile

```typescript
// Fix 1: Change 'const' to 'let' if username needs to be reassigned later.
let username: string = "code_ninja_99";
username = "senior_dev_2026"; // Now valid
// Fix 2: Age expects a number, not a string ("25"). Remove quotes.
let age: number = 25;

// Fix 3: Booleans must be true or false, not 1 or 0.
let isEmployed: boolean = true;

// Fix 4: Type inference made skills a string[] array. You cannot push a number (404).
let skills: string[] = ["HTML", "CSS", "JS"];
skills.push("TS"); // Push a string instead
```

---

### Solution 2: Strict Array Typing

```typescript
let itemNames: string[] = ["Keyboard", "Mouse", "Monitor"];
let itemPrices: number[] = [49.99, 25.50, 199.99];
let inStockFlags: boolean[] = [true, true, false];

// Error: Argument of type 'string' is not assignable to parameter of type 'number'.
// itemPrices.push("Free");
```

---

### Solution 3: The Danger of `any`

1. **Compiler check:** No, TypeScript will **not** throw an error during compilation. The `any` type disables type checking entirely for that variable.
2. **Runtime behavior:** At runtime, `mysteryData` holds the number `999`. Numbers do not have a `.split()` method in JavaScript. The program will **crash** with a `TypeError: mysteryData.split is not a function`.
3. **Safe rewrite using `unknown`:**

```typescript
let mysteryData: unknown = "Hello World";
mysteryData = [10, 20, 30];
mysteryData = 999;

// Type narrowing check
if (typeof mysteryData === "string") {
  mysteryData.split(","); // Safe! TypeScript knows it is a string inside this if-block.
}
```
