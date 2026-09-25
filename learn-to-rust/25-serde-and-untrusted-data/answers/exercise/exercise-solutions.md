# Exercise Solutions: Module 25

Attempt the exercises before reading.

## 1. Trace

No. The type accepts u64, but domain validation defines the acceptable operational range.

## 2. Repair

Return or match the serde_json::Error at the boundary rather than converting malformed external data into panic.

## 3. Modify

Derive Serialize and Deserialize on the enum and choose a documented external naming representation if persistence compatibility matters.

## 4. Build

Treat format version as part of the compatibility contract. Parse first, then reject unsupported versions and excessive or invalid domain data.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
