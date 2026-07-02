# Module 04 Quiz Answers

Detailed answers for Module 04 quiz.

---

### Answer 1
- For `val: UnionAB`, you **cannot** safely access `val.name` directly. Since `val` might be `{ age: 20 }` (type `B`), accessing `.name` causes a compiler error until narrowed.
- For `val2: IntersectionAB`, you **can** safely access `val2.name` directly. An intersection (`A & B`) guarantees the variable possesses all properties from both types simultaneously.

---

### Answer 2
A shared literal property (the discriminator) allows the TypeScript compiler to use standard JavaScript control flow (`switch` or `if/else` checks on `obj.status`) to instantly narrow the union to a single specific shape without requiring complex `in` or `typeof` property inspection checks.

---

### Answer 3
TypeScript throws a compiler error inside the `default` block: `Type '"West"' is not assignable to type 'never'.`  
Because `"West"` was unhandled in the `switch`, `dir` narrows down to `"West"` inside the default block rather than `never`. Assigning anything other than `never` to a `never` typed variable causes a compile error, guaranteeing that developers cannot forget to handle new union cases.

---

### Answer 4
If a function returns `boolean`, calling it (`if (isFish(pet))`) only evaluates to true or false; TypeScript's compiler inside the `if` block still treats `pet` as its original type (`any` or union).  
When using a type predicate (`pet is Fish`), TypeScript's compiler recognizes the check and automatically **narrows** `pet` to `Fish` inside any scope where the function returned `true`.
