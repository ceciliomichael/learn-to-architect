# Module 04 Quiz: Advanced Types & Narrowing

Write your reasoning inside the **ANSWER HERE** blocks below.

---

### Question 1: Intersection vs Union
If you have:
```typescript
type A = { name: string };
type B = { age: number };
type UnionAB = A | B;
type IntersectionAB = A & B;
```
If you receive a variable `val: UnionAB`, can you safely access `val.name` without checking its type first? What about `val2: IntersectionAB` accessing `val2.name`?

#### ✍️ ANSWER HERE:
> UnionAB behavior: 
> IntersectionAB behavior: 

---

### Question 2: Discriminated Unions
Why is a shared literal property (like `status: "loading" | "success"`) critical when defining discriminated unions, compared to having completely disjoint properties?

#### ✍️ ANSWER HERE:
> Explanation: 

---

### Question 3: Exhaustiveness Checking with `never`
Look at this code:
```typescript
type Direction = "North" | "South" | "East";

function getAngle(dir: Direction): number {
  switch (dir) {
    case "North": return 0;
    case "South": return 180;
    default:
      const _exhaustiveCheck: never = dir;
      return _exhaustiveCheck;
  }
}
```
If another developer later adds `"West"` to `Direction`, what happens when they compile this code? Why?

#### ✍️ ANSWER HERE:
> What happens during compilation & Why: 

---

### Question 4: Custom Type Guard Return Types
What is the difference between writing `function isFish(pet: any): boolean` and `function isFish(pet: any): pet is Fish`?

#### ✍️ ANSWER HERE:
> Difference: 
