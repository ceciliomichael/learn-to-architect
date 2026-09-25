# Exercise Solutions: Module 22

Attempt the exercises before reading.

## 1. Trace

No. map creates a lazy adapter. Work occurs when a consumer asks it for items.

## 2. Repair

Use an appropriate consumer. The choice should match the desired output rather than collect everything automatically.

## 3. Modify

Use iter().copied().filter(...).map(...).sum::<i32>().

## 4. Build

Both an iterator chain and loop are valid. Compare which makes filtering, ownership conversion, and output intent easiest to read.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
