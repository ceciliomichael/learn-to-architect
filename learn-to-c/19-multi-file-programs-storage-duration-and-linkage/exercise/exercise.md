# Exercise: Multi-File Programs, Storage Duration, and Linkage

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Create convert.h declaring int minutes_to_seconds(int minutes).
2. Create convert.c including the header and defining that function.
3. Create main.c including the header and printing the result for 3.
4. Compile both source files separately with strict C17 warnings.
5. Link both object files and run the program.

## Success check

Both translation units use one shared declaration, exactly one definition is linked, and the program prints 180.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

