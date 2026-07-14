# Exercise: Preprocessor, Includes, Macros, and Generic Selection

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Define a parenthesized SQUARE(value) macro that evaluates its argument twice by expansion.
2. Use it only with the side-effect-free value 6 and print 36.
3. Write a comment in your own notes explaining why SQUARE(index++) is unsafe.
4. Use _Generic to distinguish int and float values.
5. Compile the preprocessed output with -E and locate the expanded square expression.

## Success check

The macro argument has no side effect, expansion is fully parenthesized, the result is 36, and generic selection names both demonstrated types.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

