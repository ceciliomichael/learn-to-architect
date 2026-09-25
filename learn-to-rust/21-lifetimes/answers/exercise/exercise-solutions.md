# Exercise Solutions: Module 21

Attempt the exercises before reading.

## 1. Trace

No. The returned reference's validity must fit the referent it can point to; it cannot outlive that data.

## 2. Repair

Return owned String. Ownership moves to the caller and no dangling relationship is created.

## 3. Modify

Keep the owning String alive in main while Excerpt uses a slice of it. The containing borrowed value cannot outlive the owner.

## 4. Build

Return the first non-empty borrowed input or None. The lifetime parameter states that any returned reference is derived from those inputs.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
