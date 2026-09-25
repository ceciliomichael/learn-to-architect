# Exercise Solutions: Module 15

Attempt the exercises before reading.

## 1. Trace

The final content is [1, 2]. push adds 3 and pop removes the last element.

## 2. Repair

Iterate over &values for shared access or &mut values for element mutation while retaining the vector.

## 3. Modify

Mutate through &mut iteration, then perform a separate shared iteration and branch before printing.

## 4. Build

Keep one Vec<String> owner. add takes &mut Vec<String>, list can take &[String], and remove must validate the index before Vec::remove.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
