# Exercise Solution: Threads, Atomics, and Memory Ordering

```c
#include <stdatomic.h>
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

static int increment(void *argument)
{
    atomic_int *counter = argument;
    for (int index = 0; index < 7500; ++index) {
        (void)atomic_fetch_add_explicit(
            counter, 1, memory_order_relaxed);
    }
    return 0;
}

int main(void)
{
    atomic_int counter = ATOMIC_VAR_INIT(0);
    thrd_t worker;
    if (thrd_create(&worker, increment, &counter) != thrd_success) {
        return EXIT_FAILURE;
    }
    (void)increment(&counter);

    int result = 0;
    if (thrd_join(worker, &result) != thrd_success || result != 0) {
        return EXIT_FAILURE;
    }
    printf("%d\n", atomic_load_explicit(
        &counter, memory_order_relaxed));
    return EXIT_SUCCESS;
}
```

## Why it works

Both paths safely update one live atomic counter, the join completes before the read, and the result is 15000. The relevant inputs, boundaries, and failures remain visible.

