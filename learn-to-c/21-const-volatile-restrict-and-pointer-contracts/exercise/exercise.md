# Exercise: const, volatile, restrict, and Pointer Contracts

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Write a copy_values function accepting a count, const int *restrict source, and int *restrict destination.
2. Copy exactly count elements.
3. Call it with two distinct arrays of three elements.
4. Print the destination.
5. State why volatile would not make overlapping buffers safe.

## Success check

The source is read-only through its parameter, the two arrays satisfy the restrict promise, and the copied output is 4 8 12.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

