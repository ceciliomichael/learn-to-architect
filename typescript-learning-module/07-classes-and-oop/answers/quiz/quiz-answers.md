# Module 07 Quiz Answers

Detailed answers for Module 07 quiz.

---

### Answer 1: Yes!
**Explanation:** TypeScript access modifiers (`private`, `protected`, `public`) are compile-time annotations only. When compiled to standard JavaScript, the property becomes a normal object property accessible to any runtime JavaScript code. (Note: Modern ES private fields denoted with `#` like `#secretKey` *do* enforce real JavaScript runtime privacy).

---

### Answer 2:
- `private` properties are only accessible inside the exact class where they are defined. Subclasses extending the class cannot access them.
- `protected` properties are accessible inside the defining class AND inside any child subclass that extends it.

---

### Answer 3:
No, attempting `new MyAbstractClass()` causes a compiler error. Abstract classes serve as blueprints intended solely to be subclassed by child classes, providing shared functionality while requiring children to implement missing abstract methods.

---

### Answer 4: No.
**Explanation:** The `implements` keyword is strictly a compile-time check ensuring the class provides implementations matching every signature in the interface. It does not emit or inherit any runtime logic or default property values.
