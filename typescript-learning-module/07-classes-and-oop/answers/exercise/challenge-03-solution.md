# Challenge 03 Solution: Abstract Classes and Interfaces

## Executive Summary & Learning Objectives
This solution illustrates the powerful combination of **Interfaces** (`implements`) and **Abstract Classes** (`abstract`). In enterprise engineering, interfaces define pure behavioral contracts across unrelated classes, while abstract classes provide foundational blueprints that combine shared implementations with mandatory abstract method requirements. This challenge demonstrates polymorphism and structural compliance in complex domain hierarchies.

## Complete Production-Ready Code

```typescript
// 1. Structural Contract Interface: Defines WHAT a class must do, without any implementation
export interface Printable {
  print(): void;
}

// 2. Abstract Base Class: Serves as an uninstantiable blueprint combining shared logic and contracts
export abstract class Shape implements Printable {
  // Abstract methods: No body allowed; child subclasses are strictly forced to implement these!
  public abstract getArea(): number;
  public abstract print(): void;

  // Concrete method: Fully implemented logic shared automatically by all child subclasses
  public describe(): void {
    console.log(`[SHAPE DESCRIPTION]: This geometric shape has a calculated area of ${this.getArea().toFixed(2)} units squared.`);
  }
}

// 3. Concrete Subclass: Circle
export class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  public getArea(): number {
    return Math.PI * this.radius * this.radius;
  }

  public print(): void {
    console.log(`[PRINT]: Drawing a circle with radius ${this.radius}.`);
  }
}

// 4. Concrete Subclass: Rectangle
export class Rectangle extends Shape {
  constructor(public width: number, public height: number) {
    super();
  }

  public getArea(): number {
    return this.width * this.height;
  }

  public print(): void {
    console.log(`[PRINT]: Drawing a rectangle of dimensions ${this.width} x ${this.height}.`);
  }
}

// Runtime Execution & Polymorphic Verification
const shapes: Shape[] = [
  new Circle(5),
  new Rectangle(8, 3)
];

console.log("--- Executing Polymorphic Shape Operations ---");
for (const shape of shapes) {
  shape.describe(); // Executes shared base logic, which dynamically calls subclass getArea()
  shape.print();    // Executes specialized subclass print logic
}

// COMPILER ERROR DEMONSTRATION:
// const invalidShape = new Shape();
// Error: Cannot create an instance of an abstract class.
```

## Symbol-by-Symbol Breakdown Table

| Symbol / Keyword | Type / Nature | Architectural Role & Meaning |
| :--- | :--- | :--- |
| `interface` | Structural Blueprint | Pure compile-time contract. Erased completely during JavaScript compilation; enforces method signatures across classes. |
| `abstract class` | Base Class Blueprint | A class structure that cannot be instantiated directly with `new`. Exists solely to be subclassed via `extends`. |
| `abstract method` | Signature Requirement | A method signature inside an abstract class without a body. Forces every concrete child subclass to provide an implementation. |
| `implements` | Contract Adoption | Instructs TypeScript to verify that the class publicly implements all properties and methods defined on the target interface. |
| `Shape[]` | Polymorphic Array Type | An array typed to hold any object instance inheriting from `Shape`, enabling polymorphic iteration and execution. |
| `toFixed(2)` | Number Method | Formats the numeric area calculation to exactly two decimal places for clean presentation. |

## Architectural Trade-offs & Design Decisions

### 1. Why Combine `abstract class Shape implements Printable`?
By having the abstract class implement `Printable`, we guarantee that every single subclass of `Shape` (whether `Circle`, `Rectangle`, or a future `Polygon`) automatically adopts the `Printable` contract. Furthermore, because `print()` is declared as an `abstract` method on `Shape`, the TypeScript compiler ensures that no developer can create a concrete shape subclass without writing custom printing logic.

### 2. Abstract vs. Interface for Base Modeling
Why not use an interface for `Shape`? If `Shape` were purely an interface (`interface Shape`), we could not include the concrete `describe()` method! Every subclass would be forced to duplicate the exact same `console.log("This shape has an area of " + ...)` logic. Abstract classes solve this trade-off by allowing us to share reusable helper methods (`describe`) while still mandating customized implementations for domain-specific calculations (`getArea`).

## Common Pitfalls & Anti-Patterns

* **Attempting to Instantiate Abstract Classes**: Writing `new Shape()` is illegal. Abstract classes represent incomplete architectural concepts. The compiler blocks instantiation to prevent runtime errors from calling unimplemented abstract methods.
* **Forgetting `super()` in Subclass Constructors**: Even if an abstract parent class has an empty constructor or no explicit constructor arguments, derived subclasses must still invoke `super()` inside their constructor before referencing `this`.
* **Omitting Access Modifiers on Implemented Methods**: When implementing an interface method in a class, the method must be `public`. Marking an implemented interface method as `private` or `protected` violates the public contract defined by the interface.

## Runtime Behavior & Output Verification

When compiled and executed, the script produces the following console output:
```text
--- Executing Polymorphic Shape Operations ---
[SHAPE DESCRIPTION]: This geometric shape has a calculated area of 78.54 units squared.
[PRINT]: Drawing a circle with radius 5.
[SHAPE DESCRIPTION]: This geometric shape has a calculated area of 24.00 units squared.
[PRINT]: Drawing a rectangle of dimensions 8 x 3.
```
This confirms that polymorphic iteration successfully dispatches calls to the correct subclass implementations at runtime.
