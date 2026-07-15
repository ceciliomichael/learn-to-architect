# Exercises: Synchronization and the Race Detector

1. Create an intentionally racy counter in disposable test code and observe `go test -race`.
2. Repair the counter with a private mutex.
3. Return worker subtotals and sum them in one owner instead of sharing a total.
4. Use `sync.Once` for immutable initialization.
5. Document a lock invariant and one consistent lock order.
