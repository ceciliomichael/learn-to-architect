# Exercise Solutions: Module 30

Attempt the exercises before reading.

## 1. Trace

Every element has the same outer Box<dyn Formatter> type while the boxed concrete values differ. Vec<Upper> has one concrete element type only.

## 2. Repair

Move generic construction outside the dynamic interface or replace it with a concrete/object-safe return contract. The right redesign depends on what runtime behavior is actually needed.

## 3. Modify

Implement Formatter for Lower and push a boxed Lower into the same vector. The loop depends only on the trait contract.

## 4. Build

Keep Reporter small. Domain/application logic calls the trait method; tests can inject an in-memory implementation and production can inject console output.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
