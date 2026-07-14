# Quiz answers

1. It finishes after every sender is dropped and all queued messages are received.
2. `Arc` shares ownership; `Mutex` controls mutable access.
3. It records that a thread panicked while holding the lock, so protected state may be inconsistent.
4. Short scopes reduce contention and make deadlocks less likely.
5. Acquire locks in the same order everywhere.
