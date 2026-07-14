# Quiz Answers: Functions, Scope, and Header Declarations

1. **What does a function declaration provide?**

   It provides the function name, return type, and parameter types before a call is checked.

2. **How are ordinary arguments passed in C?**

   They are passed by value, so each parameter receives a copy.

3. **Where is a block variable visible?**

   From its declaration to the end of the enclosing block, subject to nested declarations that may hide it.

4. **Why mark a file-only helper static?**

   It gives the function internal linkage so its name does not collide with helpers in other source files.

5. **Must a definition match its earlier declaration?**

   Yes. A mismatch violates the function's type contract and requires a diagnostic.

