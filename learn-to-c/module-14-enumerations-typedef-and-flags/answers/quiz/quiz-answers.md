# Quiz Answers: Enumerations, typedef, and Flags

1. **Does an enum variable automatically reject every unlisted integer?**

   No. Validate values that cross an untrusted or weakly typed boundary.

2. **What does typedef do?**

   It introduces another name for an existing type.

3. **How are two flags combined?**

   Use bitwise OR.

4. **How is one required flag tested?**

   Use bitwise AND and compare the result with zero or with the complete required mask.

5. **Why use distinct powers of two for flags?**

   Each option then occupies an independent bit and can be combined or removed without changing the others.

