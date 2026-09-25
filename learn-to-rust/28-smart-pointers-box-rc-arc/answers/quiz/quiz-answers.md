# Quiz Answers: Module 28

## 1

It introduces fixed-size pointer indirection so the recursive containing type has a known size.

## 2

No. It increments the strong ownership count for the same allocation.

## 3

Its reference-count operations are not designed for cross-thread synchronization and it does not implement the required thread-safety traits.

## 4

No. Arc provides shared ownership; mutation needs a separate safe strategy.

## 5

A set of strong reference-counted owners that keep each other alive even when no external owner can reach them.
