# Module 02 Quiz: Custom Types & Interfaces

Write your answers inside the **ANSWER HERE** blocks below each question.

---

### Question 1: Declaration Merging
What happens if you declare two interfaces with the exact same name in the same file?

```typescript
interface UserSettings {
  theme: string;
}

interface UserSettings {
  fontSize: number;
}
```

A) TypeScript throws a duplicate identifier compiler error.  
B) The second declaration completely overwrites the first declaration.  
C) TypeScript automatically merges them into one interface requiring both `theme` and `fontSize`.  
D) Only `fontSize` is kept at runtime.

#### ✍️ ANSWER HERE:
> Choice: 
> Explanation: 

---

### Question 2: `type` vs `interface`
Which of the following is true regarding `type` aliases and `interface` declarations? (Select all that apply)

A) Only `interface` can describe the shape of a JavaScript object.  
B) `interface` supports declaration merging, whereas `type` does not.  
C) `type` can represent primitive union types (like `type Status = "open" | "closed"`), whereas `interface` cannot.  
D) At runtime, objects typed with `interface` execute faster than objects typed with `type`.

#### ✍️ ANSWER HERE:
> Choices: 
> Explanation: 

---

### Question 3: Optional vs. `undefined`
Look at these two object shapes:

```typescript
interface ShapeA {
  description?: string;
}

interface ShapeB {
  description: string | undefined;
}
```

If you create an object `const obj: ShapeA = {}` (omitting `description` entirely), it succeeds. What happens if you try `const objB: ShapeB = {}`? Why?

#### ✍️ ANSWER HERE:
> What happens & Why: 

---

### Question 4: Structural Duck Typing
Look at the following code:
```typescript
interface Point2D {
  x: number;
  y: number;
}

const point3D = { x: 10, y: 20, z: 30 };
const myPoint: Point2D = point3D;
```
Will `const myPoint: Point2D = point3D;` throw a compiler error? Why or why not?

#### ✍️ ANSWER HERE:
> Answer & Explanation: 
