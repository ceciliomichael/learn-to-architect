# Module 04: Advanced Types and Narrowing

In real programs, data is not always a predictable single type. A function might receive either a string or a number. An API response might be a success with data or an error with a message. This module teaches you how TypeScript handles those situations safely.

---

## 1. Union Types: "This or That"

A union type says a variable can hold one of several types. You write it using the `|` pipe symbol between types
```typescript
let id: string | number;

id = "user-abc"; // Valid.
id = 12345;      // Valid.
// id = true;    // ERROR! boolean is not in the union.
```

The important thing to understand is that TypeScript will only let you use features that are guaranteed to exist on ALL possible types in the union. If you have `string | number`, you cannot call `.toUpperCase()` directly, because numbers do not have that method.

```typescript
function printId(id: string | number): void {
  // id.toUpperCase(); // ERROR! This might be a number.
  console.log(id); // Safe. Both strings and numbers can be logged.
}
```

To use type-specific methods, you must first narrow down the type using a check.

---

## 2. Intersection Types: "This and That"

An intersection type combines multiple types into one. The variable must satisfy ALL the combined types at once. You write it using the `&` symbol
```typescript
type HasName = { name: string };
type HasAge  = { age: number };

type Person = HasName & HasAge;

// This object must have BOTH name AND age
const alice: Person = { name: "Alice", age: 30 };
```

Union (`|`) means either one. Intersection (`&`) means both at once.

---

## 3. Literal Types: Restricting to Exact Values

Instead of allowing any string, you can restrict a variable to a specific set of exact text values. These are called **literal types**
```typescript
type Direction = "North" | "South" | "East" | "West";

let heading: Direction = "North"; // Valid.
// let bad: Direction = "Up";     // ERROR! "Up" is not part of the allowed values.
```

Literal types are extremely useful because they let TypeScript catch typos and invalid values at compile time. You will see this pattern everywhere in professional code.

---

## 4. Type Narrowing

Type narrowing is the process of writing a check that proves to TypeScript which specific type a variable is at a given point in the code. Once TypeScript is convinced, it gives you access to all the methods and properties of that specific type.

### Narrowing with `typeof`

The `typeof` operator (covered in Module 01) returns a string describing the type. You use it inside an `if` statement to narrow
```typescript
function formatValue(value: string | number): string {
  if (typeof value === "string") {
    // Inside this block, TypeScript knows 'value' is definitely a string.
    return value.toUpperCase();
  } else {
    // Inside this block, TypeScript knows 'value' is definitely a number.
    return value.toFixed(2);
  }
}

console.log(formatValue("hello")); // "HELLO"
console.log(formatValue(9.99));    // "9.99"
```

### Narrowing with `in`

The `in` operator checks whether a specific property name exists inside an object. This is how you narrow between object types that have different properties
```typescript
interface Car  { drive(): void; fuelType: string; }
interface Boat { sail(): void;  anchorWeight: number; }

function operateVehicle(vehicle: Car | Boat): void {
  if ("fuelType" in vehicle) {
    // 'fuelType' only exists on Car, so TypeScript narrows to Car here.
    vehicle.drive();
  } else {
    // TypeScript knows it must be a Boat at this point.
    vehicle.sail();
  }
}
```

---

## 5. Custom Type Guards

Sometimes `typeof` and `in` are not enough to narrow a complex type. You can write your own type guard function. A type guard returns a `boolean`, but its return type is written as a special **type predicate** using the `is` keyword. This tells TypeScript exactly what type the variable is if the function returns `true`
```typescript
interface Cat  { meow(): void;  lives: number; }
interface Bird { chirp(): void; wingspan: number; }

// The return type 'pet is Cat' is the type predicate
function isCat(pet: Cat | Bird): pet is Cat {
  return (pet as Cat).meow !== undefined;
}

function handlePet(pet: Cat | Bird): void {
  if (isCat(pet)) {
    // TypeScript narrows 'pet' to Cat inside this block
    pet.meow();
  } else {
    // TypeScript narrows 'pet' to Bird inside this block
    pet.chirp();
  }
}
```

Without the `is Cat` predicate, TypeScript would just see a `boolean` return and would not narrow the type inside the `if` block.

---

## 6. The `switch` Statement

A `switch` statement is a cleaner alternative to a long chain of `if / else if / else` blocks when you are checking the same variable against multiple possible values
```typescript
type Status = "active" | "inactive" | "banned";

function describeStatus(status: Status): string {
  switch (status) {
    case "active"
      return "User is currently active.";
    case "inactive"
      return "User has not logged in recently.";
    case "banned"
      return "User has been banned.";
    default
      return "Unknown status.";
  }
}
```

Each `case` is checked against the value of `status`. When a match is found, that block runs and TypeScript stops checking the rest.

---

## 7. Discriminated Unions

A discriminated union is a pattern where every type in a union shares a common property with a unique literal value. That shared property is called the **discriminant**. This lets TypeScript instantly and reliably narrow the union in a `switch` statement
```typescript
type LoadingState = { status: "loading" };
type SuccessState = { status: "success"; data: string[] };
type ErrorState   = { status: "error"; message: string; code: number };

type RequestState = LoadingState | SuccessState | ErrorState;
```

Every member of the union has a `status` property, but each `status` is a different literal string. TypeScript uses that to narrow perfectly
```typescript
function renderUI(state: RequestState): string {
  switch (state.status) {
    case "loading"
      return "Loading...";
    case "success"
      return "Loaded " + state.data.length + " items."; // 'data' is available here.
    case "error"
      return "Error " + state.code + ": " + state.message; // 'message' and 'code' are available here.
  }
}
```

Notice that inside each `case`, TypeScript automatically knows which specific type `state` is. Inside `case "success"`, it knows `state.data` exists. Inside `case "error"`, it knows `state.message` exists. This is the main benefit of discriminated unions.

---

## 8. The `never` Type and Exhaustiveness Checking

`never` represents a value that should never exist. If a function has `never` as a return type, it means the function never successfully returns (it always throws an error or loops forever).

More practically, `never` is used as a safety net inside discriminated union switch statements. If you add a new state to a union but forget to handle it in a `switch`, TypeScript will tell you by producing a type error
```typescript
function renderUI(state: RequestState): string {
  switch (state.status) {
    case "loading"
      return "Loading...";
    case "success"
      return "Loaded data.";
    case "error"
      return "Error occurred.";
    default
      // If 'state' reaches here, TypeScript knows something is wrong.
      // If all cases are handled, 'state' is of type 'never' at this point.
      // If a new status is added to RequestState but not handled above, TypeScript
      // will give an error here because that new type is not 'never'.
      const exhaustiveCheck: never = state;
      return exhaustiveCheck;
  }
}
```

This pattern ensures you can never accidentally forget to handle a new case in the future.

---

## 9. Type Casting (`as`)

Sometimes you know more about a value's type than TypeScript does. You can use the `as` keyword to tell TypeScript to treat a value as a specific type. Use this carefully and only when you are certain
```typescript
let value: unknown = "Hello World";

// TypeScript won't let you call string methods on 'unknown' directly.
// But if you are certain it is a string, you can cast it
let length = (value as string).length;
console.log(length); // Outputs: 11
```

Type casting does not change the actual data. It only changes what TypeScript thinks about the data at compile time.

A common real-world use is narrowing the return type of `JSON.parse`, which TypeScript types as `any`
```typescript
const raw: unknown = JSON.parse('{"name":"Alice","age":30}');
const user = raw as { name: string; age: number };
console.log(user.name); // "Alice"
```

Use `as` only when you have good reason to trust the shape. If you are wrong, TypeScript will not protect you  -  the error happens at runtime.

---

## 10. The Non-Null Assertion Operator (`!`)

The `!` operator is placed directly after a value that TypeScript thinks might be `null` or `undefined`. It tells TypeScript: "I know for certain this is not null or undefined. Do not warn me about it."

```typescript
function getElement(id: string): HTMLElement {
  const el = document.getElementById(id);
  // TypeScript says: 'el' could be HTMLElement | null
  // The ! asserts: "trust me, it exists"
  return el!;
}
```

The non-null assertion does nothing at runtime. It only silences TypeScript's warning. If you are wrong and the value is actually `null`, your code will crash at runtime with a `TypeError`.

**When to use it:** Only in situations where you have external knowledge that TypeScript cannot infer  -  for example, a DOM element that you know will always exist because your HTML guarantees it.

**When NOT to use it:** Whenever you could simply write an `if` check instead. If in doubt, check first.

```typescript
// Prefer this (safe at runtime)
const el = document.getElementById("app");
if (el === null) {
  throw new Error("Element #app not found in the DOM.");
}
el.style.display = "block"; // TypeScript narrows to HTMLElement here.

// Over this (dangerous if wrong)
document.getElementById("app")!.style.display = "block";
```

---

## 11. Enums

An **enum** (short for enumeration) is a way to define a set of named constants as a group. TypeScript supports two kinds.

### String Enums

String enums are the most common in modern TypeScript. Each member has an explicit string value
```typescript
enum Direction {
  North = "NORTH",
  South = "SOUTH",
  East  = "EAST",
  West  = "WEST"
}

let heading: Direction = Direction.North;
console.log(heading); // "NORTH"

// heading = "UP"; // ERROR! "UP" is not part of the Direction enum.
```

### Numeric Enums

Numeric enums auto-assign numbers starting from 0 if you do not give explicit values
```typescript
enum Priority {
  Low,      // 0
  Medium,   // 1
  High,     // 2
  Critical  // 3
}

let taskPriority: Priority = Priority.High;
console.log(taskPriority); // 2
```

### Enums vs Literal Union Types

Both accomplish similar goals. The key difference is that enums generate real JavaScript code at runtime  -  the `Direction` object actually exists in the compiled output. Literal union types are erased completely.

```typescript
// Enum  -  generates a real object
enum Status { Active = "ACTIVE", Inactive = "INACTIVE" }

// Literal union  -  purely a compile-time concept, zero runtime cost
type Status = "ACTIVE" | "INACTIVE";
```

Modern TypeScript teams increasingly prefer literal union types for simple cases because they produce cleaner, smaller JavaScript. Use enums when you specifically need the runtime object  -  for example, when iterating over all possible values or when the enum is used in many files and you want a single source of truth with a named group.

```typescript
// Iterating an enum (requires numeric enum or Object.values tricks)
enum Color { Red = "RED", Green = "GREEN", Blue = "BLUE" }
const allColors = Object.values(Color); // ["RED", "GREEN", "BLUE"]
```

---
