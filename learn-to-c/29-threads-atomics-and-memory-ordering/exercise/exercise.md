# Exercise: Threads, Atomics, and Memory Ordering

This exercise requires a C17 implementation that provides `threads.h`. If yours does not, complete the reasoning on paper and rerun the program with a supporting toolchain before treating it as verified.

## Steps

1. Create one worker and increment in main too.
2. Perform 7500 increments on each path.
3. Join before reading the final counter.
4. Use a relaxed atomic only for the independent count.
5. Verify 15000.

## Success check

Both paths safely update one live atomic counter, the join completes before the read, and the result is 15000.
