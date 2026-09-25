# Exercise Solutions: Module 16

Attempt the exercises before reading.

## 1. Trace

The existing value becomes 3; the default is not inserted.

## 2. Repair

Use the map as the owner and borrow data through lookup. Clone only if independent owned copies are genuinely required.

## 3. Modify

Iterate over split_whitespace and increment each entry using entry(...).or_insert(0).

## 4. Build

Use the map for product-to-quantity association and the set for uniqueness of discontinued codes. Keep ownership in the collections.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
