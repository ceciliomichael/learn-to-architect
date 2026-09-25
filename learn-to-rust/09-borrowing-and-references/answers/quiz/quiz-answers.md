# Quiz Answers: Module 09

## 1

Ownership is responsibility for a value and its resource lifetime; borrowing is temporary access to a value owned elsewhere.

## 2

Yes, when no conflicting mutation is active.

## 3

They could create conflicting writes or read/write aliasing that makes reasoning and safety difficult.

## 4

No. It refers to a value owned elsewhere unless the reference is itself stored inside another owned structure.

## 5

No. The compiler can end a borrow after its last use when the relationship is no longer needed.
