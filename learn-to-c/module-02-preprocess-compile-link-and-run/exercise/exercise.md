# Exercise: Preprocess, Compile, Link, and Run

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Save the example as main.c.
2. Create preprocessed output with gcc -std=c17 -E main.c -o main.i.
3. Compile only with gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow -c main.c -o main.o.
4. Link with gcc main.o -o main, then run it.
5. Change doubled to tripled in both its definition and call, rebuild every stage, and print 63.

## Success check

The separate compile and link commands succeed, and the executable prints 63.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

