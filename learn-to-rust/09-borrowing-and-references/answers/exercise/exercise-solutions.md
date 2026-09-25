# Exercise Solutions: Module 09

Attempt the work first.

## 1. Trace

text owns the String. a and b are shared borrowers. Neither owns the String, and both can read it while their borrows are valid.

## 2. Repair

Arrange the code so the mutable reference's last use occurs before the original value is used again, or use a smaller block when that makes the intended lifetime clearer.

## 3. Modify

fn length(text: &str) -> usize works for string slices and is more general. Passing &message can coerce to &str.

## 4. Build

Keep ownership in main. Pass &mut text to the mutating function and &text or text.as_str() to read-only logic. No clone is needed.

Equivalent designs can be correct when they satisfy the same rules and behavior.
