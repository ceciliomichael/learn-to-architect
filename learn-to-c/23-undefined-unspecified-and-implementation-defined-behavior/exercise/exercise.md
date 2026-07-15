# Exercise: Undefined, Unspecified, and Implementation-Defined Behavior

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Print CHAR_BIT, CHAR_MIN, and CHAR_MAX.
2. Compute the unsigned width from sizeof(unsigned) and CHAR_BIT.
3. Shift 1U by width - 1 and print the result.
4. Write down why shifting by width would be undefined.
5. Compile once normally and once with optimization, expecting equivalent defined output.

## Success check

Every reported property comes from the implementation, and the only shift count used is strictly less than the unsigned width.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

