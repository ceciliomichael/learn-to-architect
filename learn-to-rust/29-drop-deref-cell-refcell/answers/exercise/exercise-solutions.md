# Exercise Solutions: Module 29

Attempt the exercises before reading.

## 1. Trace

Cell is an interior-mutability abstraction whose API permits controlled replacement through shared access. Its safety contract does not hand out conflicting references to the interior value.

## 2. Repair

End or drop the first RefMut guard before requesting another borrow. The same many-readers-or-one-writer rule still applies.

## 3. Modify

Borrow the Vec briefly, clone it, then return the independent Vec. The clone is justified if callers need an owned snapshot after the borrow ends.

## 4. Build

The spy can push a call description into a private RefCell from a shared trait method. Tests can expose a separate snapshot/read method rather than exposing the RefCell itself.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
