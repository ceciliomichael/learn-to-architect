# Exercise: Enumerations, typedef, and Flags

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Define an enum Mode with MODE_READ and MODE_EDIT.
2. Define flag constants FEATURE_SEARCH and FEATURE_EXPORT using separate bits.
3. Create a mask containing both features.
4. Test each feature with bitwise AND and print enabled when present.
5. Remove FEATURE_EXPORT and prove its test is then false.

## Success check

The choices and flags have separate roles, both flags begin enabled, and only export is removed.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

