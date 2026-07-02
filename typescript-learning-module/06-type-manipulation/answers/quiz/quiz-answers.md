# Module 06 Quiz Answers

Detailed answers for Module 06 quiz.

---

### Answer 1: B
**Explanation:** `keyof` extracts the property keys of an object interface and returns them as a literal string union: `"volume" | "muted"`.

---

### Answer 2
No, `typeof` in a type context (`type T = typeof myVariable;`) does **not** execute at runtime. It is purely evaluated by the TypeScript compiler during compilation to inspect the static type of `myVariable` and assign it to `T`. It is completely erased from the compiled JavaScript output.

---

### Answer 3: C
**Explanation:** `Record<Keys, Type>` constructs an object type whose keys are specified by the first union argument (`"admin" | "guest"`) and whose property values are specified by the second argument (`number`).

---

### Answer 4: B
**Explanation:** TypeScript uses bracket syntax (`Person["address"]`) for indexed access type lookups. Dot notation (`Person.address`) is invalid in type declarations.
