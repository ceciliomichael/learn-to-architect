# Exercise Solutions: Module 08

Attempt the work first.

## 1. Trace

a owns the String first. After let b = a, b owns it and a is no longer usable as a value.

## 2. Repair

Use only b after the move, or reorganize ownership so the original is not needed. Clone only if two independent owned Strings are actually required.

## 3. Modify

Passing by value moves the String into consume, so the caller cannot use the original binding afterward unless ownership is returned.

## 4. Build

There are many valid arrangements. The important part is that every move and clone has a stated purpose rather than being used to silence diagnostics.

Equivalent designs can be correct when they satisfy the same rules and behavior.
