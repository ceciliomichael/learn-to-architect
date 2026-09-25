# Exercise Solutions: Module 28

Attempt the exercises before reading.

## 1. Trace

Three strong owners exist: the original plus two clones.

## 2. Repair

Use Arc and clone the Arc for the worker. Arc's count is atomic, but the inner type still must satisfy thread transfer/sharing requirements.

## 3. Modify

Pattern-match through borrowed list nodes and recurse or loop over the Box indirection without consuming the list.

## 4. Build

Strong child ownership expresses that parents keep children alive. Weak parent references allow upward navigation without keeping ancestors alive solely because descendants reference them.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
