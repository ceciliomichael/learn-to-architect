# Challenge 04 Solution: Union Types in Action

This solution demonstrates how to architect polymorphic data identifiers using TypeScript Union Types and how to perform safe runtime type narrowing using `typeof` type guards.

---

## 1. Complete Production Implementation

```typescript
// Define a reusable type alias representing an identifier that can be text or numeric
type UserId = string | number;

// 1. Declare a variable with our union type and initialize it with a string
let currentId: UserId = "usr-84920-x";

// Perform runtime type narrowing before invoking string-specific methods
if (typeof currentId === "string") {
  // Within this block, TypeScript narrows currentId from 'string | number' strictly to 'string'
  console.log(currentId.toUpperCase()); // Outputs: "USR-84920-X"
}

// 2. Reassign the variable to a numeric value (valid under the union contract)
currentId = 40401;

// Perform runtime type narrowing before performing numeric concatenation/logic
if (typeof currentId === "number") {
  // Within this block, TypeScript narrows currentId strictly to 'number'
  console.log("Numeric ID: " + currentId.toFixed(0)); // Outputs: "Numeric ID: 40401"
}
```

---

## 2. Symbol-by-Symbol Breakdown

Let us deconstruct the union type declaration and narrowing logic:

* `type` -> Built-in keyword instructing TypeScript to declare a new custom type alias.
* `UserId` -> Custom PascalCase identifier representing our union type.
* `=` -> Binding operator linking the name to the type expression.
* `string` -> Primitive type representing text values.
* `|` -> The Union Operator (read as "OR"). In type theory, this indicates that a value can satisfy either the type on the left OR the type on the right.
* `number` -> Primitive type representing integer or floating-point numbers.
* `typeof` -> Built-in JavaScript unary operator that evaluates the runtime data type of a variable and returns a string string representation (e.g., `"string"`, `"number"`, `"boolean"`, `"object"`).
* `===` -> Strict equality operator verifying both value and type identity without type coercion.

---

## 3. Architectural Trade-offs & Runtime Implications

### Why Union Types Require Type Narrowing (Type Guards)
When a variable is typed as a union (`string | number`), TypeScript adopts a strict safety posture: **you can only directly access properties or methods that are common to EVERY type in the union**.
* **The Constraint:** If you try to call `currentId.toUpperCase()` directly without an `if` statement, TypeScript throws a fatal compiler error (`Property 'toUpperCase' does not exist on type 'number'`). Even if you just assigned a string to it one line earlier, when working with complex function parameters typed as unions, the compiler cannot guarantee which type is present without explicit runtime checks.
* **The Solution (Type Narrowing):** Using JavaScript's native `typeof` operator inside a control flow block (`if (typeof val === "string")`) acts as a **Type Guard**. TypeScript's compiler performs control flow analysis: it reads the `if` condition and intelligently narrows the type of `currentId` from `string | number` down to `string` inside that specific scope.

### Why You MUST Use `type` Instead of `interface` for Unions
As established in our architectural rules, this is a fundamental differentiator between Interfaces and Type Aliases:
* **Interfaces are strictly for Object shapes:** An interface declares a structural contract of key-value pairs. You cannot write `interface UserId = string | number;` because an interface cannot name a primitive or union value.
* **Type Aliases are universal type expressions:** The `type` keyword can assign a name to *any* valid type expression, including primitives, unions (`A | B`), intersections (`A & B`), tuples (`[string, number]`), and complex conditional functions.

### Real-World Enterprise Use Case: API Payload Tolerance
In legacy REST APIs or microservice architectures, database records often undergo migrations over decades. In an old system, a customer ID might be stored as an auto-incrementing integer (`40401`), whereas in a newer modern microservice, IDs are generated as UUID strings (`"usr-84920-x"`). By typing frontend network layer DTOs (Data Transfer Objects) as `id: string | number`, your application can seamlessly ingest payloads from both legacy and modern backend services without breaking JSON deserialization.
