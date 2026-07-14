# Exercise: Pointers, Addresses, and Null

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Write a static reset function accepting int *value.
2. If value is not NULL, assign zero through the pointer.
3. In main, create an int initialized to 42 and pass its address.
4. Print the changed value.
5. Call reset(NULL) to confirm the function's documented null behavior.

## Success check

The caller's object changes to zero, and the null call performs no dereference.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

