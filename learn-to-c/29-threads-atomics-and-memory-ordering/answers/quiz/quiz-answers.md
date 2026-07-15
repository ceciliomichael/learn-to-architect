# Quiz Answers: Threads, Atomics, and Memory Ordering

1. **What is a data race?**

   Conflicting unsynchronized accesses to one non-atomic object from multiple threads.

2. **Does volatile prevent it?**

   No.

3. **Why is relaxed ordering enough here?**

   Only the numeric update needs indivisibility, and no other data is published through it.

4. **What must happen to a joinable thread?**

   Its owner must join it before dependent state is released.

5. **When is a mutex clearer?**

   When several fields form one invariant that must change or be observed together.

