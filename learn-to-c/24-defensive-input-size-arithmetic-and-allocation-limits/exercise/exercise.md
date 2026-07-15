# Exercise: Defensive Input, Size Arithmetic, and Allocation Limits

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Parse the text 64 into a size_t.
2. Reject invalid syntax, ERANGE, values above SIZE_MAX, and counts above 128.
3. Before allocating doubles, check count against SIZE_MAX / sizeof(double).
4. Treat a null result as failure when count is nonzero.
5. Free the allocation and print the accepted count.

## Success check

The syntax, type range, policy limit, multiplication, allocation result, and cleanup are all handled, and 64 is accepted.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

