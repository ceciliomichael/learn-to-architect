# Exercise: Formatted Input and Output

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Create a 40-byte buffer for a favorite food.
2. Prompt on stdout, then read with fgets.
3. On failure, write a clear diagnostic to stderr and return EXIT_FAILURE.
4. On success, print You chose: followed by the stored line.
5. Test ordinary input and end-of-input.

## Success check

Success and failure take different paths, input is bounded by the array size, and no format warning appears.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

