# Quiz Answers: Module 29

## 1

Resource acquisition and cleanup are tied to object lifetime so destruction releases the resource deterministically.

## 2

It enforces shared/exclusive borrow rules dynamically at runtime instead of entirely at compile time for the interior value.

## 3

Invalid overlapping borrows are detected while running and cause a panic.

## 4

No. It is a single-threaded abstraction; synchronization types come later.

## 5

When a sound API genuinely needs mutation behind shared access and ordinary ownership or &mut would make the design worse or impossible.
