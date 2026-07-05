# Question 03: Structural Typing vs Nominal Typing

TypeScript uses structural typing (often called Duck Typing or shape-based compatibility). In this question, you will analyze two scenarios demonstrating how TypeScript compares data types.

---

## Part 1: Object Literal Assignment & Excess Properties

Consider the following code:
```typescript
interface Point2D {
  x: number;
  y: number;
}

const point3D = {
  x: 10,
  y: 20,
  z: 30
};

const point: Point2D = point3D;
```

1. Does `const point: Point2D = point3D;` produce a TypeScript compiler error? Why or why not?
2. The object `point3D` has an extra property (`z`) that is not defined in `Point2D`. Why does TypeScript allow assigning it to a `Point2D` variable when passed via an intermediate reference?
3. What would happen if `point3D` was missing the `y` property?

---

## Part 2: Classes vs Interfaces across Different Names

In nominal languages like Java or C++, types are checked by their explicit brand names and declaration hierarchies. Consider this TypeScript code:

```typescript
interface Swimmer {
  swimSpeed: number;
}

class Dolphin {
  swimSpeed: number;
  constructor(speed: number) {
    this.swimSpeed = speed;
  }
}

function race(swimmer: Swimmer): void {
  console.log(`Racing at speed: ${swimmer.swimSpeed}`);
}

const flipper = new Dolphin(25);
race(flipper);
```

4. Notice that `Dolphin` never explicitly implements `Swimmer` (`class Dolphin implements Swimmer` is omitted). Does calling `race(flipper)` cause a compiler error? Why or why not?
5. How does this structural evaluation differ from nominal typing systems?

---

## ANSWER HERE

> **Part 1: Does assigning point3D to point produce an error? Why?**

> **Part 1: Why does TypeScript allow extra properties via variable reference?**

> **Part 1: What happens if property y is missing?**

> **Part 2: Does passing a Dolphin instance into race(Swimmer) cause an error?**

> **Part 2: How does this differ from nominal typing systems?**
