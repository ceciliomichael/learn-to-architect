# Module 05 Quiz Answers Master Reference

This master reference document provides exhaustive, production-grade conceptual answers for all Module 05 quiz questions. Each explanation covers compilation mechanics, symbol-by-symbol breakdowns, memory behavior, and architectural best practices.

---

## Question 01 Answer: any vs. Generics

### Why Generics are Superior to `any`
* **Using `any`**: When a function is typed as `function processAny(arg: any): any`, the TypeScript compiler turns off static type checking completely. If you pass a string `"hello"` and subsequently call `result.toFixed(2)`, the compiler raises zero errors. However, at runtime, evaluating `"hello".toFixed(2)` throws a fatal crash: `TypeError: result.toFixed is not a function`.
* **Using Generics `<T>`**: When a function is typed as `function processSafe<T>(arg: T): T`, the compiler captures the exact input type (such as `string`) and binds it to `T`. Calling `result.toFixed(2)` triggers an immediate compile-time error: `Property 'toFixed' does not exist on type 'string'`.
* **Memory & Runtime Behavior**: Due to **Type Erasure**, generics exist purely at compile time. Transpiled to JavaScript, both functions have identical bare-metal runtime execution speed and zero memory overhead.

---

## Question 02 Answer: Generic Constraints (`extends`)

### Why Unconstrained Generics Reject Property Lookups
When declaring `<T>` without a constraint, `T` could represent any possible type in existence (such as a `number` or `boolean`). Because primitives do not possess a `.length` property, accessing `item.length` is flagged by the compiler as a potential runtime error.

### The Fix Using `extends`
```typescript
function getLength<T extends { length: number }>(item: T): number {
  return item.length; // Safe! TypeScript guarantees .length exists.
}
```
* **Structural Subtyping**: This constraint accepts any data type possessing a numeric `.length` property, including strings (`"hello"`), arrays (`[1, 2, 3]`), and custom domain objects (`{ id: 1, length: 100 }`), while rejecting numbers (`42`) and plain objects (`{ name: "Alice" }`).

---

## Question 03 Answer: Multiple Type Variables (`<T, K, V>`)

### Why Enterprise Architectures Require Multiple Type Variables
When modeling key-value pairs or dictionary mappings (`function createPair<K, V>(key: K, value: V): { key: K; value: V }`), declaring two independent type parameters decouples the key's type from the value's type.
* **Polymorphic Flexibility**: Allows heterogeneous pairings such as `<string, number>` for user scores or `<number, boolean>` for HTTP status flags.
* **Engineering Conventions**: Standard developer conventions use **`T`** for primary domain Types, **`K`** for property Keys, **`V`** for dictionary Values, and **`E`** for array Elements.

---

## Question 04 Answer: Generic Inference & `keyof` Constraints

### Generic Inference & Indexed Access Types
* **Type Inference**: When calling `getProperty(workstation, "brand")` without angle brackets, TypeScript inspects the arguments and automatically infers `T -> Laptop` and `K -> "brand"`.
* **The `keyof` Constraint**: The signature `K extends keyof T` enforces that `K` must strictly match one of the public property names of object `T` (for `Laptop`, `"brand" | "ramGigabytes" | "isTouchscreen"`). Attempting to pass `"graphicsCard"` results in an immediate compile-time error.
* **Indexed Access (`T[K]`)**: Typing the return value as `T[K]` guarantees that requesting `"brand"` returns a `string`, while requesting `"ramGigabytes"` returns a `number`. This pattern protects enterprise data-fetching and state management engines from property lookup bugs with zero runtime reflection overhead.
