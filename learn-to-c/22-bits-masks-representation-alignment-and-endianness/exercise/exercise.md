# Exercise: Bits, Masks, Representation, Alignment, and Endianness

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Create a uint32_t mask with bits 1 and 5 set.
2. Print it in eight hexadecimal digits.
3. Clear bit 1 and prove bit 5 remains set.
4. Print sizeof and alignof for uint32_t.
5. Explain why these values alone do not define a portable binary file format.

## Success check

The original mask is 0x00000022, the final mask is 0x00000020, and bit 5 remains set.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

