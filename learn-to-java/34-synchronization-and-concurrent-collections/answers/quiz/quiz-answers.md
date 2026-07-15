# Quiz answers

1. A data race can lose updates or expose stale state even when individual reads look harmless.
2. synchronized provides mutual exclusion and a happens-before relationship around the same monitor.
3. Keep critical sections short and never hold a lock across slow external I/O.
4. ConcurrentHashMap supports concurrent access but multi-step domain rules may still need atomic map methods.
5. Atomic classes suit focused counters and flags, not arbitrary multi-field invariants.

