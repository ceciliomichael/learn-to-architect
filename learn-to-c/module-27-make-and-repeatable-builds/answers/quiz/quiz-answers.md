# Quiz Answers: Make and Repeatable Builds

1. **When does Make rebuild a target?**

   When it is missing or older than a prerequisite.

2. **What begins a recipe line?**

   A tab character in traditional Make syntax.

3. **What belongs in CFLAGS?**

   C compiler options such as standard, warnings, optimization, and debug settings.

4. **Why list project headers as prerequisites?**

   A header change can change an object and must trigger recompilation.

5. **Why is clean phony?**

   It names an action rather than a file to update.

