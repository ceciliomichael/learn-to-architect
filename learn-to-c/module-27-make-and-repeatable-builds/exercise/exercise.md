# Exercise: Make and Repeatable Builds

## Steps

1. Create a two-file program with one header.
2. Use the strict C17 flags in a Makefile.
3. Declare both object and header dependencies.
4. Add a phony clean target.
5. Build twice, change one implementation, and observe the rebuild.

## Success check

One command uses the declared flags, an unchanged second build compiles nothing, and clean removes only generated files.

