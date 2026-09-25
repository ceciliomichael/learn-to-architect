# Exercises: Module 36

Work locally and explain your choices.

## 1. Trace

Why does Arc<Mutex<T>> need both Arc and Mutex? What problem does each solve?

## 2. Repair

Lock the same non-reentrant Mutex twice while the first guard is live, then shorten the first guard's scope.

## 3. Modify

Change the counter example so each worker increments a local variable and acquires the shared lock once to add its subtotal.

## 4. Build

Design a small shared cache with Arc<RwLock<HashMap<String,String>>>. Specify read/write operations, lock scope, poison policy, and why a message-passing owner thread might instead be simpler.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
