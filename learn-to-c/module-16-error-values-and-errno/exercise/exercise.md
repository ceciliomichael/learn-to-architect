# Exercise: Error Values and errno

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Reuse the parse_int pattern to parse the text -17.
2. Require a non-NULL result pointer in your function and fail if it is NULL.
3. Reject the strings hello, 12x, and an integer larger than INT_MAX.
4. Accept surrounding whitespace.
5. Print the accepted value.

## Success check

The parser accepts the complete valid value, rejects partial and out-of-range text, and writes the result only on success.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

