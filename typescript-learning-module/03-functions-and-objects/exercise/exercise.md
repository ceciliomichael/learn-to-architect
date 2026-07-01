# Module 03 Exercise: Functions & Typing Signatures

Complete your code directly inside the **ANSWER HERE** blocks below.

---

### Challenge 1: Strongly Typed Calculator
Write a function called `calculate` that accepts three parameters:
1. `operation`: Must be typed strictly as the literal union `"ADD" | "SUBTRACT" | "MULTIPLY" | "DIVIDE"`.
2. `a`: A number.
3. `b`: A number.

The function must return a `number`. If `operation` is `"DIVIDE"` and `b === 0`, throw an `Error("Cannot divide by zero")`.

#### ✍️ ANSWER HERE:
```typescript
// Write your calculate function here:


```

---

### Challenge 2: Optional Parameters vs Default Parameters
Write two functions that format a user greeting:
1. `formatGreetingOptional(name: string, title?: string): string`: If `title` is provided, return `"Hello [title] [name]"`. Otherwise, return `"Hello [name]"`.
2. `formatGreetingDefault(name: string, title: string = "Explorer"): string`: Return `"Hello [title] [name]"`. Notice what happens when you pass `undefined` as the second argument when calling this function!

#### ✍️ ANSWER HERE:
```typescript
// Write your formatting functions here:


```

---

### Challenge 3: Function Overloads for Flexible Parsers
Write function overload signatures for a function called `parseCoordinate`:
1. If passed two numbers (`x: number, y: number`), it returns `{ x: number, y: number }`.
2. If passed a single coordinate string formatted as `"x,y"` (e.g., `"10,20"`), it returns `{ x: number, y: number }`.

Write the overload signatures above the implementation, and then write the single implementation function that handles both cases using `typeof`.

#### ✍️ ANSWER HERE:
```typescript
// Write your overload signatures and implementation here:


```
