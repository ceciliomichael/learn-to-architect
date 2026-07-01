# Module 01 Quiz Answers

Review your answers against the detailed explanations below.

---

### Answer 1: B
**Explanation:** TypeScript is purely a **development-time** tool. When `tsc` compiles your `.ts` files into `.js` files, every type annotation (`: string`, `interface`, `type`) is completely erased. The JavaScript engine (V8, Node.js, browsers) runs pure JavaScript without knowing TypeScript ever existed.

---

### Answer 2: No, TypeScript will NOT throw an error.
**Explanation:** `const` prevents **variable reassignment** (e.g., trying to do `scores = [100, 200]`). However, arrays and objects stored in a `const` variable are still **mutable in memory**. You can mutate the contents of the array (pushing, popping, modifying items at indices) without changing the variable's reference.

---

### Answer 3:
**Error message:** `Type 'boolean' is not assignable to type 'string'.`  
**Why no explicit type was needed:** When you assign an initial value upon declaration (`let currentStatus = "Loading"`), TypeScript uses **Type Inference** to deduce that `currentStatus` should permanently be a `string`. Explicitly typing `: string` is optional when declaring and initializing on the same line.

---

### Answer 4: B and C
**Explanation:**  
- **B & C are correct:** TypeScript catches type mismatches immediately in your IDE and creates strict contracts that make codebase maintenance and team collaboration much safer.  
- **A & D are incorrect:** TypeScript does not optimize networking speed or provide runtime data encryption.
