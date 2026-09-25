# Exercise Solutions: Module 07

Attempt the work first.

## 1. Trace

Position 0 is a string slice and position 1 is an integer. let (direction, distance) = pair destructures them.

## 2. Repair

Index 3 is the fourth position and is out of bounds for length 3. get returns Option so missing data can be handled explicitly.

## 3. Modify

Initialize a mutable total to zero and iterate over the array, adding each value. Iterator details come later; a direct for loop is enough.

## 4. Build

Use [f64; 7] or another suitable numeric type, iterate over the readings, and use get for the uncertain index.

Equivalent designs can be correct when they satisfy the same rules and behavior.
