# Question 01 Answer: Union vs. Intersection Mechanics

## 1. Executive Summary and Direct Answers

Given the following type definitions:
```typescript
type A = { name: string };
type B = { age: number };
type UnionAB        = A | B;
type IntersectionAB = A & B;
```

### 1. You have `val: UnionAB`. Can you safely write `val.name` without a check? Why?
**No, you cannot safely access `val.name` directly.** 
In TypeScript, a Union Type (`A | B`) guarantees only that the variable satisfies *at least one* of the constituent type blueprints. At compile time, TypeScript does not know whether `val` currently holds an object matching `A` (`{ name: "Alice" }`) or an object matching `B` (`{ age: 30 }`). Because `B` does not possess the property `name`, attempting to access `val.name` without first verifying its presence triggers a fatal compiler error: `Property 'name' does not exist on type 'UnionAB'. Property 'name' does not exist on type 'B'.`

### 2. You have `val2: IntersectionAB`. Can you safely write `val2.name` without a check? Why?
**Yes, you can safely access `val2.name` directly without any runtime checks.**
An Intersection Type (`A & B`) synthesizes a unified type blueprint that must possess **all** properties from **every** constituent type simultaneously. A valid object of type `IntersectionAB` is guaranteed by the compiler to contain both `name: string` AND `age: number`. Therefore, accessing `val2.name` (or `val2.age`) is 100% safe and verified at compile time.

### 3. Real-World Analogies
- **Union Analogy (`|`):** A union is like a **mystery gift box** labeled "Contains either a hardbound book OR a coffee mug." You cannot try to drink coffee from it or turn its pages until you open the box and verify which item is actually inside!
- **Intersection Analogy (`&`):** An intersection is like a **Swiss Army Knife** that is simultaneously a folding blade AND a can opener AND a screwdriver. It possesses every tool from every category built into one single physical object, ready to be used immediately without checking.

---

## 2. Complete Production-Grade Code Examples

Below is a complete, runnable demonstration contrasting safe versus unsafe property access on Union and Intersection types.

```typescript
type A = { name: string };
type B = { age: number };
type UnionAB        = A | B;
type IntersectionAB = A & B;

/**
 * Demonstrates safe handling of a Union type using property narrowing.
 *
 * @param val - An object that is either type A or type B.
 */
function processUnion(val: UnionAB): void {
  // --- UNSAFE ACCESS (Would cause compile error if uncommented) ---
  // console.log(val.name); // COMPILER ERROR: Property 'name' does not exist on type 'B'.

  // --- SAFE ACCESS VIA NARROWING GATE ---
  // We use the 'in' operator to check if property "name" exists in the runtime object.
  if ("name" in val) {
    // Inside this block, Control Flow Analysis narrows 'val' strictly to type A.
    console.log(`Union contains name: ${val.name.toUpperCase()}`);
  } else {
    // In the else block, TypeScript knows 'val' must be type B.
    console.log(`Union contains age: ${val.age.toFixed(0)}`);
  }
}

/**
 * Demonstrates direct, unconditional access on an Intersection type.
 *
 * @param val2 - An object possessing all properties of both A and B.
 */
function processIntersection(val2: IntersectionAB): void {
  // Because val2 is an intersection, BOTH properties are guaranteed to exist.
  // Zero narrowing checks are required!
  console.log(`Intersection user: ${val2.name} is ${val2.age} years old.`);
}

// --- Comprehensive Runtime Test Cases ---
const onlyA: UnionAB = { name: "System Admin" };
const onlyB: UnionAB = { age: 45 };
const bothAB: IntersectionAB = { name: "Lead Architect", age: 38 };

processUnion(onlyA);       // Output: "Union contains name: SYSTEM ADMIN"
processUnion(onlyB);       // Output: "Union contains age: 45"
processIntersection(bothAB); // Output: "Intersection user: Lead Architect is 38 years old."
```

---

## 3. Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Name | Technical Role and Significance |
| :--- | :--- | :--- |
| `A \| B` | **Union Type Operator** | Logical "OR" in type theory. Represents a value that satisfies type A, type B, or both. Restricts un-narrowed property access to shared properties only. |
| `A & B` | **Intersection Type Operator** | Logical "AND" in type theory. Synthesizes a new type requiring all properties from both A and B to be present simultaneously on a single object. |
| `"name" in val` | **Property Existence Guard** | The runtime `in` operator checks whether the string key `"name"` exists in the object's property prototype chain. Used by TypeScript for type narrowing. |
| `val.name` | **Property Accessor** | Evaluates object property lookup. Blocked by the compiler on unions unless the property is shared across all union members or narrowed first. |

---

## 4. Deep Technical Explanation: Underlying Type Theory

To master advanced TypeScript, you must understand how the compiler models types using **Set Theory**.

### Union Types as Set Union ($A \cup B$)
When you declare `type UnionAB = A | B;`, think of type `A` as the set of all objects containing `name: string`, and type `B` as the set of all objects containing `age: number`. The union type is the combined set of all objects belonging to either set.
- Why can't you access `.name` directly? Because an object residing in set $B$ (e.g., `{ age: 20 }`) is a valid member of the union set, but it lacks the `.name` property.
- **The Shared Property Rule:** Before narrowing, TypeScript only allows you to access the intersection of properties (that is, properties that exist on *every single member* of the union). Since `A` and `B` share no common property keys, zero properties can be accessed directly on `UnionAB`!

### Intersection Types as Set Intersection ($A \cap B$)
When you declare `type IntersectionAB = A & B;`, you are demanding that an object belong to set $A$ AND set $B$ simultaneously.
- What object belongs to both sets? Only an object that contains *both* `name: string` AND `age: number`!
- Therefore, the synthesized blueprint for `IntersectionAB` is effectively `{ name: string; age: number; }`. Because every valid object must contain all properties, the compiler permits unconditional access to `.name` and `.age`.

---

## 5. Runtime and Memory Analysis

### Zero Memory Overhead for Type Combinations
Both Union (`|`) and Intersection (`&`) type operators are strictly **compile-time type annotations**.
- During the TypeScript compilation phase, the type checking engine verifies all property accesses and assignment rules.
- Once compilation completes, all type annotations, type aliases (`A`, `B`, `UnionAB`, `IntersectionAB`), and union/intersection symbols are completely stripped from the emitted JavaScript.
- In V8 or Node.js runtime memory, an object of type `IntersectionAB` is stored simply as a standard JavaScript Object: `{"name":"Lead Architect","age":38}`. It consumes the exact same heap memory as a raw JavaScript object literal, with zero runtime wrapper classes or metadata overhead.

---

## 6. Concrete Anti-Patterns vs. Best Practices

### Anti-Pattern: Forcing Property Access via Unsafe Type Casting
Junior developers often get frustrated by union property restrictions and bypass the compiler using `as` type casts.
```typescript
// BAD: Forcing the compiler to ignore potential missing properties!
function badUnionHandler(val: UnionAB): void {
  // If 'val' is actually { age: 30 }, (val as A).name evaluates to undefined!
  // Calling .toUpperCase() on undefined throws a fatal runtime TypeError!
  console.log((val as A).name.toUpperCase());
}
```

### Best Practice: Safe Property Narrowing via the `in` Operator
Always use structured runtime checks to prove property existence before accessing member-specific fields on a union.
```typescript
// GOOD: Safe, verified runtime narrowing!
function goodUnionHandler(val: UnionAB): void {
  if ("name" in val) {
    console.log(val.name.toUpperCase());
  } else {
    console.log(`User age is ${val.age}`);
  }
}
```

---

## 7. Architectural Trade-offs

| Type Combination | Pros | Cons | Enterprise Best Use Case |
| :--- | :--- | :--- | :--- |
| **Union Types (`\|`)** | Highly flexible; allows modeling polymorphic data, API responses with error states, and optional configurations without forcing all data into one giant object. | Requires runtime narrowing checks (`in`, `typeof`, `switch`) before accessing member-specific properties; can become unwieldy if union members lack shared discriminator tags. | Modeling API responses (`Success \| Error`), UI component loading states, and polymorphic function parameters. |
| **Intersection Types (`&`)** | Enables clean composition of modular type blueprints; eliminates code duplication across type definitions; allows unconditional property access. | Creating impossible intersections (e.g., merging `{ id: string } & { id: number }`) silently collapses property types to `never`; can produce complex, hard-to-read error messages in deep hierarchies. | Composing middleware request objects in Express/NestJS (`Request & AuthUser & SessionData`), merging database entity timestamps with domain models. |
