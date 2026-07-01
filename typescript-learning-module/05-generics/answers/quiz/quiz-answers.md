# Module 05 Quiz Answers

Detailed explanations for Module 05 quiz.

---

### Answer 1:
- For `processA("hello")`, the return type is `any`. TypeScript loses all type tracking; you could call `.toFixed()` on the result without any compile-time error.
- For `processB("hello")`, the return type is strictly inferred as `string` (or `"hello"`). TypeScript maintains exact type safety from input to output.

---

### Answer 2:
TypeScript throws an error because `T` can represent **any** type (such as a `number` or `boolean`), which do not possess a `.length` property.  
To fix it, constrain `T` using `extends`: `function getLength<T extends { length: number }>(item: T): number`.

---

### Answer 3:
For `p`, `K` is explicitly `string` and `V` is explicitly `number`.  
Yes! Because `Pair<K, V>` is generic, another instance can independently pass entirely different type arguments like `Pair<boolean, string[]>`.

---

### Answer 4:
TypeScript performs **Generic Type Argument Inference**. By inspecting the argument passed in (`42`), the compiler automatically infers that `T` should be bound to `number`.
