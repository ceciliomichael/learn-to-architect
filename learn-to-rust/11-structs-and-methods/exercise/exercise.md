# Exercises: Module 11

Use a local Cargo project. Predict first.

## 1. Trace

For a method fn name(&self) -> &str, explain what the method borrows and whether it can normally mutate fields.

## 2. Repair

Write a method using &self that increments a numeric field, observe the error, and change the receiver appropriately.

## 3. Modify

Add deactivate(&mut self) to Account and include the result in summary.

## 4. Build

Build a BankAccount struct with owner and balance, plus deposit, can_withdraw, withdraw, and summary methods. Reject withdrawals larger than the balance without allowing a negative result.

Finish with cargo fmt, cargo clippy, and cargo check.
