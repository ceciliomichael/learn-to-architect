# Exercise Solutions: Module 36

Attempt the exercises before reading.

## 1. Trace

Arc provides multiple owners across threads; Mutex provides exclusive synchronized access to mutable T. Neither substitutes for the other's responsibility.

## 2. Repair

Let the first guard drop before requesting another lock. In multi-lock designs, also establish consistent acquisition order.

## 3. Modify

Compute 1,000 locally, then lock once and add 1,000. This dramatically reduces lock acquisition and contention while preserving the total.

## 4. Build

Reads can take a read guard and clone or derive the needed result before releasing it; writes take a write guard. Compare this with one cache-owning thread receiving commands if lock complexity grows.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
