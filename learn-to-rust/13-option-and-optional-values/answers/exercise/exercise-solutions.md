# Exercise Solutions: Module 13

Attempt the work first.

## 1. Trace

It can be None or Some containing a u32. Some(0) is present value zero; None is no value.

## 2. Repair

Return Option and use values.first().copied() or explicit empty handling. The type now tells callers absence is possible.

## 3. Modify

Iterate with enumerate and return Some(index) when the value is even; return None after the loop.

## 4. Build

Iterate with enumerate, compare each name to target, return Some(index) on a match, and None otherwise.

Equivalent designs can be correct when they satisfy the same rules and behavior.
