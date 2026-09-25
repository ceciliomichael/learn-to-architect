# Exercise Solutions: Module 11

Attempt the work first.

## 1. Trace

It shares the instance through a read-only borrow. Ordinary fields cannot be mutated through that receiver.

## 2. Repair

Use &mut self for an in-place mutation, and ensure the caller's binding is mutable when invoking the method.

## 3. Modify

Set active to false in deactivate. summary already includes active and should reflect the changed field.

## 4. Build

Use methods to keep the balance rules near the data. can_withdraw can use &self, while deposit and successful withdraw require &mut self.

Equivalent designs can be correct when they satisfy the same rules and behavior.
