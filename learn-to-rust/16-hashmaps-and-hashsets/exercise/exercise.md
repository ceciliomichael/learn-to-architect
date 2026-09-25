# Exercises: Module 16

Work locally and explain your choices.

## 1. Trace

If x already maps to 2, what does *map.entry("x").or_insert(0) += 1 produce?

## 2. Repair

Move String key/value into a map and try to use old bindings. Repair by accessing the map rather than cloning automatically.

## 3. Modify

Create a frequency map from a sentence split on whitespace.

## 4. Build

Build inventory quantities in HashMap<String,u32> plus a HashSet<String> of discontinued codes.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
