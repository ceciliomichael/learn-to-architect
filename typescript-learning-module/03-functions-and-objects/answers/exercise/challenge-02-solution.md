# Challenge 02 Solution: Optional and Default Parameters

This document provides the exhaustive production-grade solution, symbol-by-symbol analysis, and architectural trade-offs for **Challenge 02: Optional and Default Parameters**.

---

## 1. Complete Production Implementation

```typescript
// Function 1: Utilizing an Optional Parameter (?)
function greetOptional(name: string, title?: string): string {
  if (title !== undefined) {
    return `Hello, ${title} ${name}`;
  }
  return `Hello, ${name}`;
}

// Function 2: Utilizing a Default Parameter (=)
function greetDefault(name: string, title: string = "Traveler"): string {
  return `Hello, ${title} ${name}`;
}

// Verification and Testing: greetOptional
console.log(greetOptional("Alice", "Dr.")); // Outputs: "Hello, Dr. Alice"
console.log(greetOptional("Alice"));         // Outputs: "Hello, Alice"

// Verification and Testing: greetDefault
console.log(greetDefault("Bob", "Captain")); // Outputs: "Hello, Captain Bob"
console.log(greetDefault("Bob"));            // Outputs: "Hello, Traveler Bob"
```

---

## 2. Symbol-by-Symbol Analysis

### Deconstructing Optional Syntax (`title?: string`)
* `title`: Developer-assigned parameter identifier representing the honorific.
* `?`: Optional modifier symbol. In the TypeScript Abstract Syntax Tree (AST), this transforms the parameter's type from strictly `string` into the union type `string | undefined`. It instructs the compiler that omitting this argument at call site is valid.
* `:`: Type annotation anchor.
* `string`: The required data type if the argument is supplied by the caller.

### Deconstructing Default Syntax (`title: string = "Traveler"`)
* `title`: Developer-assigned parameter identifier.
* `:`: Type annotation anchor.
* `string`: Required data type constraint.
* `=`: Default assignment operator. During runtime execution, if the argument passed is `undefined` (or omitted entirely), the JavaScript engine evaluates this operator and assigns the fallback value.
* `"Traveler"`: The literal string fallback value assigned when no argument is provided.

---

## 3. Architectural Trade-Offs and Best Practices

### When to Choose Optional (`?`) vs. Default (`=`)
* **Optional Parameters (`?`)**: Use when the absence of a value carries a distinct semantic meaning. In `greetOptional`, having no title means the user does not possess an honorific; therefore, rendering `"Hello, Alice"` without a placeholder title is architecturally correct.
* **Default Parameters (`=`)**: Use when a system requires a guaranteed fallback value to operate seamlessly. In `greetDefault`, the business logic dictates that every user must be addressed with a title; if none is provided, the system defaults to `"Traveler"`.

### The Mandatory Parameter Ordering Rule
As emphasized in Section 2 of the README, an optional parameter marked with `?` cannot be followed by a required parameter. You cannot declare `function badOrder(title?: string, name: string)`.
Why? When the JavaScript runtime executes a function call like `badOrder("Alice")`, arguments are bound positionally from left to right. If an optional parameter were positioned first, the engine would bind `"Alice"` to `title`, leaving `name` as `undefined` and violating the required contract of the second parameter.

### Template Literals vs. String Concatenation
In both functions, we utilize template literals (`Hello, ${title} ${name}`) instead of string concatenation (`"Hello, " + title + " " + name`). Template literals improve code maintainability, eliminate missing space bugs, and provide superior readability when constructing complex UI messages.
