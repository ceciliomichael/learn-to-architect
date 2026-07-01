# Module 03 Quiz Answers

Detailed explanations for Module 03 quiz.

---

### Answer 1: No, it will NOT throw an error.
**Explanation:** When a callback type is specified as returning `void` (`() => void`), TypeScript allows functions that return values to be passed in, but it **ignores** the returned value. This ensures compatibility with common JavaScript patterns like passing `() => array.push(x)` (where `.push()` returns a number) into `.forEach()`.

---

### Answer 2: No, external code CANNOT call `process(true)`.
**Explanation:** When function overloads are present, only the explicit **overload signatures** above the implementation are visible to outside callers. The implementation signature (`x: any`) is strictly internal to the function's implementation body and cannot be called externally.

---

### Answer 3: B
**Explanation:** Rest parameters collect all remaining passed arguments into a single JavaScript array at runtime. Therefore, their type annotation must always be an array type (`number[]` or `Array<number>`).

---

### Answer 4: Contextual Typing
**Explanation:** Standalone arrow functions (`const add = (a, b) => ...`) lack surrounding context, so TypeScript infers `a` and `b` as `any` unless explicitly typed. Inside `.map()` on a `number[]` array, TypeScript knows the array elements are numbers, allowing it to perform **Contextual Typing** to automatically type the callback parameter without explicit annotations.
