# Module 04 Quiz Answers: Master Architectural Guide

Welcome to the exhaustive master answer guide for the **Module 04 Conceptual Quiz: Advanced Types and Narrowing**. This document provides deeply technical, enterprise-grade explanations and code examples for all five quiz questions, evaluating your mental models against production engineering standards.

---

## 1. Question 01 Answer: Union vs. Intersection Mechanics

### Direct Answer
- **For `val: UnionAB` (`A | B`):** You **cannot** safely access `val.name` directly without a check. A union type guarantees only that the value matches *at least one* of the constituent types. Because `val` might hold an object of type `B` (`{ age: number }`), which lacks the property `name`, accessing `val.name` unconditionally triggers a fatal compiler error. You must narrow the type first using `if ("name" in val)`.
- **For `val2: IntersectionAB` (`A & B`):** You **can** safely access `val2.name` directly without any check. An intersection type synthesizes a unified blueprint requiring the value to possess **all** properties from **both** `A` and `B` simultaneously. The compiler guarantees that both `name` and `age` are present.
- **Real-World Analogies:**
  - **Union (`|`):** A mystery package labeled "Contains either a Laptop OR a Printer." You cannot plug in a printer cable until you open the box and verify which device is inside.
  - **Intersection (`&`):** A Swiss Army Knife that is simultaneously a blade AND a screwdriver AND a can opener. All tools are present in one body, ready for immediate use.

### Code Verification
```typescript
type A = { name: string };
type B = { age: number };

function testUnion(val: A | B): void {
  // val.name; // COMPILER ERROR: Property 'name' does not exist on type 'A | B'.
  if ("name" in val) {
    console.log(`Name: ${val.name}`); // Safe after narrowing!
  }
}

function testIntersection(val2: A & B): void {
  console.log(`Name: ${val2.name}, Age: ${val2.age}`); // 100% safe unconditionally!
}
```

---

## 2. Question 02 Answer: The `in` Operator and Interface Narrowing

### Direct Answer
The **`in` operator** is a native JavaScript relational operator (`"property" in object`) that checks whether a string property key exists on an object or in its prototype chain at runtime. In TypeScript, when used inside a conditional statement, Control Flow Analysis (CFA) hooks into this runtime check. If a property key exists on interface `VideoFile` but not on `ImageFile`, checking `"duration" in file` automatically narrows the union type strictly down to `VideoFile` inside the `if` block and strictly down to `ImageFile` in the `else` block.

### Code Verification
```typescript
interface VideoFile { duration: number; codec: string; }
interface ImageFile { width: number; height: number; }

function describeMedia(file: VideoFile | ImageFile): string {
  if ("duration" in file) {
    // TypeScript narrows 'file' strictly to VideoFile here
    return `Video: ${file.duration}s (Codec: ${file.codec})`;
  } else {
    // TypeScript narrows 'file' strictly to ImageFile here
    return `Image: ${file.width}x${file.height}px`;
  }
}
```

---

## 3. Question 03 Answer: Type Predicates (`is` Keyword) vs. Plain Booleans

### Direct Answer
- **Inside if-block with Version A (`: boolean`):** TypeScript still treats `pet` as the un-narrowed union `Cat | Dog`. A plain boolean return tells the compiler only that the function evaluated to true or false; it establishes zero semantic connection to the parameter's type state. Attempting to call `pet.meow()` triggers a compiler error.
- **Inside if-block with Version B (`: pet is Cat`):** TypeScript narrows `pet` strictly to `Cat` inside the `if` block (and strictly to `Dog` inside the `else` block). The type predicate `pet is Cat` is an explicit directive instructing Control Flow Analysis to narrow the argument across calling scopes.
- **What `pet is Cat` tells the compiler:** It provides a semantic type contract: *"If this function returns `true`, then parameter `pet` is guaranteed to satisfy the type blueprint of `Cat`."*

### Code Verification
```typescript
interface Cat { meow(): void; }
interface Dog { bark(): void; }

function isCatPredicate(pet: Cat | Dog): pet is Cat {
  return (pet as Cat).meow !== undefined;
}

function handlePet(pet: Cat | Dog): void {
  if (isCatPredicate(pet)) {
    pet.meow(); // 100% safe! Narrows strictly to Cat.
  } else {
    pet.bark(); // 100% safe! Narrows strictly to Dog.
  }
}
```

---

## 4. Question 04 Answer: The `never` Exhaustiveness Check

### Direct Answer
- **What TypeScript sees when `Triangle` is added but not handled:** In the `switch (shape.kind)` statement, `case "circle":` eliminates `Circle` and `case "square":` eliminates `Square`. When execution falls through to `default:`, the union is no longer empty! Because `Triangle` was unhandled, `shape` inside the default block has the type `{ kind: "triangle"; base: number; height: number }`.
- **The exact compiler error produced:** When attempting to execute `const check: never = shape;`, TypeScript throws:
  ```text
  Type '{ kind: "triangle"; base: number; height: number; }' is not assignable to type 'never'.
  ```
- **Why this protects the codebase:** This pattern acts as an automated compile-time circuit breaker. Without it, adding a new shape to a union would compile silently, causing functions to fall through and return `undefined` or crash at runtime. By assigning the default branch to `never`, TypeScript converts a potential silent runtime bug into an immediate build failure, forcing developers to handle every new union state across the entire codebase!

### Code Verification
```typescript
type Shape = 
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number }
  | { kind: "triangle"; base: number; height: number };

function areaExhaustive(shape: Shape): number {
  switch (shape.kind) {
    case "circle":   return 3.14 * shape.radius ** 2;
    case "square":   return shape.side * shape.side;
    case "triangle": return 0.5 * shape.base * shape.height;
    default:
      // When all cases are handled above, 'shape' is pruned to 'never'.
      // This assignment compiles cleanly with zero errors!
      const check: never = shape;
      return check;
  }
}
```

---

## 5. Question 05 Answer: Union vs. Intersection Real-World Analogy & Access Analysis

### Direct Answer
- **Part 1 (Union Guarantee & Analogy):** A union type guarantees that a value satisfies at least one of the listed type blueprints, restricting direct property access exclusively to shared members. Analogy: A sealed mystery box labeled "Contains either a Laptop OR a Printer."
- **Part 2 (Intersection Guarantee & Analogy):** An intersection type guarantees that a value simultaneously satisfies all listed type blueprints, guaranteeing that all properties from every constituent type are present. Analogy: An emergency rescue truck built as both an Ambulance AND a Fire Engine simultaneously.
- **Part 3 (Property Access Analysis):**
  - **On `u: WithEngine | WithSails` (Union):** **ZERO properties are safe to access.** Because `u` could be either vessel type, accessing `.horsepower`, `.startEngine()`, `.sailArea`, or `.hoist()` without narrowing triggers a compile error.
  - **On `i: WithEngine & WithSails` (Intersection):** **ALL FOUR properties are safe to access.** Because `i` possesses all properties from both types simultaneously, you can access `.horsepower`, `.startEngine()`, `.sailArea`, and `.hoist()` unconditionally!

### Code Verification
```typescript
type WithEngine = { horsepower: number; startEngine(): void };
type WithSails  = { sailArea: number;   hoist(): void };

function testVessels(u: WithEngine | WithSails, i: WithEngine & WithSails): void {
  // u.horsepower; // COMPILER ERROR! Must narrow first with: if ("horsepower" in u)
  
  // Safe unconditional access on intersection:
  console.log(`Hybrid Vessel HP: ${i.horsepower}, Sail Area: ${i.sailArea}`);
  i.startEngine();
  i.hoist();
}
```

---

## 6. Comprehensive Comparison Matrix: Narrowing Techniques

| Narrowing Mechanism | Syntax Pattern | Primary Use Case | Runtime Performance & Erasure |
| :--- | :--- | :--- | :--- |
| **Primitive Guard** | `typeof x === "string"` | Primitives (`string`, `number`, `boolean`, `symbol`, `bigint`). | **Ultra High Speed:** Inspects V8 internal memory type tags; zero memory allocation. |
| **Interface Guard** | `"prop" in obj` | Plain JavaScript objects and interfaces lacking literal discriminator tags. | **Very High Speed:** Checks object dictionary and prototype chain; zero metadata overhead. |
| **Discriminated Union** | `switch (obj.kind)` | State machines, asynchronous request lifecycles, and polymorphic payloads. | **Ultra High Speed:** Direct property lookup optimized by V8 Hidden Class inline caches. |
| **Custom Type Guard** | `function isX(val): val is X` | Reusable validation logic across files, array filtering (`arr.filter(isX)`). | **High Speed:** Executes custom check logic; predicate annotation erases completely at runtime. |
