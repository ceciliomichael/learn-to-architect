# Module 02 Quiz Answers

Detailed answers and reasoning for Module 02 quiz.

---

### Answer 1: C
**Explanation:** Interfaces in TypeScript undergo **Declaration Merging**. If two interfaces share the exact same name within the same scope, TypeScript merges their properties into a single combined contract. If you tried doing this with `type`, TypeScript would throw a `Duplicate identifier` error.

---

### Answer 2: B and C
**Explanation:**  
- **B & C are correct:** Interfaces are specialized for objects and support declaration merging. Type aliases are more versatile and can represent unions, primitives, tuples, or object shapes.  
- **A & D are incorrect:** Both can describe objects, and neither exists at runtime, meaning zero runtime performance difference.

---

### Answer 3: `ShapeB` throws a compiler error (`Property 'description' is missing in type '{}'`).
**Explanation:**  
When you use `?` (`description?: string`), the property itself is **optional** - the object doesn't need to have the key `description` at all.  
When you write `description: string | undefined`, the key `description` **must explicitly exist** on the object, even if its assigned value is `undefined` (e.g., `{ description: undefined }`).

---

### Answer 4: No, it will NOT throw an error.
**Explanation:** TypeScript uses **Structural Typing** (Duck Typing). When assigning `point3D` to `myPoint`, TypeScript checks if `point3D` fulfills the required structure of `Point2D`. Since `point3D` has both `x: number` and `y: number`, it satisfies the contract. Extra properties (`z: 30`) do not prevent structural compatibility during assignment from a pre-existing object variable.
