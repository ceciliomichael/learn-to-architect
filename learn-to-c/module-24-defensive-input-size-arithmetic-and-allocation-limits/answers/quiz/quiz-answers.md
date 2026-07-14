# Quiz Answers: Defensive Input, Size Arithmetic, and Allocation Limits

1. **Why is SIZE_MAX not a sufficient application limit?**

   A request can be representable yet still exhaust resources or violate the program's purpose.

2. **When should multiplication overflow be checked?**

   Before performing the multiplication.

3. **What does strtoumax provide for portable size parsing?**

   It parses into the widest standard unsigned integer type and reports the first unconverted character and range errors.

4. **Can malloc(0) return NULL without reporting failure?**

   Yes. Zero-size allocation has implementation-permitted results, so the program must define how it treats count zero.

5. **What layers should an external count pass?**

   Syntax, conversion range, destination range, application policy, size arithmetic, and actual allocation success.

