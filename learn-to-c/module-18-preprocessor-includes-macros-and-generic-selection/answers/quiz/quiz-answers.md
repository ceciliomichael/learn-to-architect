# Quiz Answers: Preprocessor, Includes, Macros, and Generic Selection

1. **When are macros expanded?**

   During preprocessing, before ordinary C type checking and code generation.

2. **Why parenthesize each macro parameter?**

   It protects the intended grouping when the caller supplies a compound expression.

3. **Why is SQUARE(index++) unsafe?**

   The macro expansion evaluates the increment expression twice, causing unsequenced or unintended side effects.

4. **What should a shared header primarily contain?**

   Declarations, type definitions, and carefully chosen macros forming the shared interface.

5. **Why can ARRAY_COUNT not accept a pointer?**

   A pointer value does not carry the number of array elements, and sizeof pointer is only the pointer object's size.

