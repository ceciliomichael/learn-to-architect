# Quiz Answers: const, volatile, restrict, and Pointer Contracts

1. **Does pointer-to-const prove no code can modify the object?**

   No. It prevents modification through that access path; another permitted non-const alias may exist.

2. **Does volatile make value++ atomic?**

   No. It neither makes the read-modify-write indivisible nor creates thread synchronization.

3. **What does restrict communicate?**

   It is a programmer promise about non-conflicting access paths for objects used through that pointer association.

4. **What happens if a restrict promise is violated?**

   The program has undefined behavior for the affected execution.

5. **Why can qualifiers improve an interface?**

   They state intended access and aliasing contracts that callers and implementations can check or use.

