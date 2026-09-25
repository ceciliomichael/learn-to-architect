# Exercise Solutions: Module 18

Attempt the exercises before reading.

## 1. Trace

No assertion or panic marks it failed, so the test runner sees success.

## 2. Repair

Use an assertion tied to the intended outcome.

## 3. Modify

Either document current integer behavior or change the API to reject negatives with Result, then test that explicit contract.

## 4. Build

Keep arithmetic logic free of I/O. Unit-test each rule and integration-test the public composition.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
