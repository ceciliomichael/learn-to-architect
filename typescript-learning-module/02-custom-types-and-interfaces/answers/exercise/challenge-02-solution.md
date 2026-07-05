# Challenge 02 Solution: Extend Blueprints Two Ways

This solution demonstrates how to achieve structural inheritance and code reuse in TypeScript using two distinct paradigms: interface inheritance via the `extends` keyword and type alias composition via the intersection (`&`) operator.

---

## 1. Complete Production Implementation

```typescript
// ==========================================
// Part 1: Inheritance via Interface Extends
// ==========================================

// 1. The base structural blueprint
interface Animal {
  name: string;
  age: number;
}

// 2. The specialized child blueprint inheriting name and age
interface Bird extends Animal {
  wingspan: number;
  canFly: boolean;
}

// 3. Instantiating a concrete Bird object matching the combined contract
const parrot: Bird = {
  name: "Polly",
  age: 5,
  wingspan: 0.4,
  canFly: true
};


// ==========================================
// Part 2: Composition via Type Intersection
// ==========================================

// 1. The base type alias
type TypeAnimal = {
  name: string;
  age: number;
};

// 2. The composed type alias intersecting base properties with bird properties
type TypeBird = TypeAnimal & {
  wingspan: number;
  canFly: boolean;
};

// 3. Instantiating a concrete TypeBird object matching the intersected shape
const eagle: TypeBird = {
  name: "Bald Eagle",
  age: 8,
  wingspan: 2.1,
  canFly: true
};
```

---

## 2. Symbol-by-Symbol Breakdown

### Interface Inheritance Syntax (`extends`)
* `interface Bird` -> Declares a new structural contract named `Bird`.
* `extends` -> Built-in keyword instructing the compiler to copy all property signatures from the specified parent interface(s).
* `Animal` -> The target parent interface whose contract is being inherited.
* `{ wingspan: number; canFly: boolean; }` -> The additional property rules unique to the child blueprint.

### Type Intersection Syntax (`&`)
* `type TypeBird` -> Declares a new custom type alias named `TypeBird`.
* `=` -> Binding operator linking the alias name to the type expression on the right.
* `TypeAnimal` -> The base type alias being referenced.
* `&` -> The Intersection Operator. In type theory, this combines multiple types into one, requiring an object to satisfy EVERY combined type simultaneously.
* `{ wingspan: number; ... }` -> An inline object literal type representing the specialized properties to merge with `TypeAnimal`.

---

## 3. Architectural Trade-offs & Decision Matrix

While both approaches produce identical object structures in memory, they possess profound architectural differences under the hood:

### 1. Compiler Performance & Caching
* **Interface `extends`:** TypeScript's type checker evaluates interfaces hierarchically. When an interface extends another, the compiler caches the relationship by name. If a type error occurs, the compiler reports the exact name of the interface (e.g., `Type 'Bird' is not assignable to...`), resulting in lightning-fast IDE autocompletion and clean error messages.
* **Type Intersection (`&`):** When intersecting type aliases, TypeScript recursively merges the properties by value during type checking. In massive enterprise codebases with deeply nested intersections, this can degrade compiler performance and produce verbose, unreadable error tooltips that expand the entire object literal shape instead of showing the alias name.

### 2. Declaration Merging
* **Interfaces:** Support declaration merging. If a third-party library defines `interface Animal`, you can declare `interface Animal { habitat: string; }` in your own code, and TypeScript will automatically merge them.
* **Type Aliases:** Are strictly closed. Declaring `type TypeAnimal` twice results in a fatal `Duplicate identifier` compiler error.

### Senior Engineer's Rule of Thumb
In production engineering, use **`interface extends`** for defining object hierarchies and domain models (Users, Products, Entities). Reserve **`type &`** for composing complex functional transformations, union unions, or utility type operations where interface syntax cannot be used.
