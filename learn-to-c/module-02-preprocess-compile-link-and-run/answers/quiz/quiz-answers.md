# Quiz Answers: Preprocess, Compile, Link, and Run

1. **What happens before C syntax is compiled?**

   The preprocessor handles directives such as include and macro replacement.

2. **What does the -c option request?**

   It asks for an object file without running the linker.

3. **Can an object file normally be run directly?**

   No. It must first be linked into an executable.

4. **What does an undefined reference usually mean?**

   The linker could not find a required definition in the supplied object files or libraries.

5. **Why rebuild after changing source?**

   An existing object file still contains code from the earlier source.

