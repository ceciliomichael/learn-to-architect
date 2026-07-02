# Challenge 03: Abstract Class and Interface Implementation

Practice abstract classes combined with interface enforcement.

## Your Tasks

1. Create an `interface Printable` with one method: `print(): void`.

2. Create an `abstract class Shape` that `implements Printable`
   - Abstract method: `getArea(): number` (no implementation  -  subclasses must provide it).
   - Abstract method: `print(): void` (satisfies the Printable interface, but must be implemented by subclasses).
   - Concrete method: `describe(): void` that logs `"This shape has an area of " + this.getArea()`.

3. Create a class `Circle` that `extends Shape`
   - Constructor takes `public radius: number` (parameter property shorthand).
   - Implement `getArea(): number` using `3.14159 * this.radius * this.radius`.
   - Implement `print(): void` that logs `"Drawing a circle with radius " + this.radius`.

4. Create a class `Rectangle` that `extends Shape`
   - Constructor takes `public width: number` and `public height: number`.
   - Implement `getArea(): number` as `this.width * this.height`.
   - Implement `print(): void` that logs `"Drawing a rectangle " + this.width + "x" + this.height`.

5. Create one `Circle` and one `Rectangle`. Call `describe()` and `print()` on both.

6. Write a commented-out line showing what happens if you try `new Shape()`.

## ANSWER HERE

```typescript
// Write your Printable interface, Shape abstract class, Circle, and Rectangle here
```
