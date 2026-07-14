# Quiz Answers: Bits, Masks, Representation, Alignment, and Endianness

1. **Why prefer unsigned types for bit manipulation?**

   Their arithmetic and shifts have clearer defined behavior, including modulo arithmetic.

2. **What shift counts are invalid?**

   Negative counts and counts at least as large as the promoted left operand's bit width.

3. **Can a structure contain padding?**

   Yes, between fields and at the end to meet alignment requirements.

4. **What does endianness describe?**

   The order of bytes used to represent a multi-byte value in memory or an external format.

5. **Why use memcpy to inspect object bytes?**

   It copies the representation through character storage without violating effective-type aliasing rules.

