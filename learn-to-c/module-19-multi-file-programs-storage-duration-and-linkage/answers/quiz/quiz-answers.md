# Quiz Answers: Multi-File Programs, Storage Duration, and Linkage

1. **What is a translation unit?**

   It is one source file after preprocessing, including the contents introduced through its directives.

2. **What does internal linkage do for a file-level helper?**

   It keeps that name private to its translation unit.

3. **How many external definitions should an ordinary function have in the linked program?**

   Exactly one.

4. **Are linkage and storage duration the same?**

   No. Linkage identifies whether declarations name the same entity; storage duration describes how long an object exists.

5. **Why include a function's own header in its implementation file?**

   The compiler can then diagnose a mismatch between the shared declaration and the definition.

