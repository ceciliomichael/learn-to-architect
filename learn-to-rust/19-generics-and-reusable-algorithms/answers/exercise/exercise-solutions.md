# Exercise Solutions: Module 19

Attempt the exercises before reading.

## 1. Trace

No. Both fields use the same T. Use separate parameters such as A and B when the fields vary independently.

## 2. Repair

Debug formatting is not guaranteed for every T. The correct repair is a Debug trait bound, introduced in Module 20.

## 3. Modify

Use struct Pair<A,B> with first: A and second: B, then implement getters returning &A and &B.

## 4. Build

Wrap Vec<T>. These operations rely on Vec behavior and need no extra trait bounds.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
