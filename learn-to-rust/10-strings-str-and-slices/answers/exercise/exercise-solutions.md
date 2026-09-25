# Exercise Solutions: Module 10

Attempt the work first.

## 1. Trace

UTF-8 may encode non-ASCII scalar values with multiple bytes. chars counts Unicode scalar values while len counts bytes.

## 2. Repair

Use text.chars().next() for the first Unicode scalar value or text.as_bytes().first() for the first byte, depending on the requirement.

## 3. Modify

The existing None branch can return text directly. The returned &str borrows from the input.

## 4. Build

Use text.len(), text.chars().count(), and text.chars().next(). The tuple contains derived data without taking ownership of the input.

Equivalent designs can be correct when they satisfy the same rules and behavior.
