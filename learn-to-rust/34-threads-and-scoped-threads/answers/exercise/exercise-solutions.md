# Exercise Solutions: Module 34

Attempt the exercises before reading.

## 1. Trace

The scope guarantees all scoped workers finish before borrowed local data can leave scope, so the lifetime relationship is statically bounded.

## 2. Repair

Use move to transfer the String into an unscoped thread when the caller no longer needs it, or use a scoped worker when borrowing is the intended relationship.

## 3. Modify

Create four non-overlapping slices, spawn one scoped worker per slice, store handles, then join and sum results before leaving the scope.

## 4. Build

Avoid shared mutable counters initially. Let each worker own its local result and combine results after joining, which reduces synchronization complexity.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
