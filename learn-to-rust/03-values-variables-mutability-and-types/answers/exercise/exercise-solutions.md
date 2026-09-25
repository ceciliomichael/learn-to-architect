# Exercise Solutions: Module 03

Read this only after attempting the exercises.

## 1. Trace

It prints 6. The second let shadows the first binding; it does not mutate the first binding.

## 2. Repair

Use a mutable binding to change one binding, or use a second let to shadow with a new binding. The two programs may print the same result but model state differently.

## 3. Modify

Initialize remaining from the constant and use remaining -= 1. No extra abstraction is necessary.

## 4. Build

A string literal, integer, floating-point value, Boolean, and char are enough. Choose narrower numeric types only when requirements justify that decision.

A different implementation can also be correct. Compare behavior, clarity, and reasoning instead of only comparing text.
