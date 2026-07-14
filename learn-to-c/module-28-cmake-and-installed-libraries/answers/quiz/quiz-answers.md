# Quiz Answers: CMake and Installed Libraries

1. **Does C define a package manager?**

   No.

2. **How do installation and discovery differ?**

   Installation places dependency files; discovery lets the build locate and describe them.

3. **Why prefer an imported CMake target?**

   It carries the complete usage requirements as one target contract.

4. **Where is the C baseline declared?**

   On the target, with extensions disabled when ISO portability is required.

5. **Why review upgrades?**

   Dependency behavior, ABI, licensing, and security are part of the program's trust boundary.

