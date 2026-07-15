# Module 29: Threads, Atomics, and Memory Ordering

## What you will learn

This module builds the next production C skill without hiding its contracts.

## Threads share memory

Shared objects must remain alive until all users finish. Every created joinable thread needs ownership and cleanup.

The C thread library is an optional part of C17. This example requires an implementation that provides `threads.h`. If the header is unavailable, use a toolchain that implements it or a clearly labeled platform thread API. Do not mistake one toolchain's missing header for a language rule, and do not present a Windows or POSIX API as portable ISO C.

## A data race is undefined behavior

Conflicting unsynchronized accesses to one non-atomic object from different threads create a data race. volatile is not synchronization.

## Atomics provide specific guarantees

An atomic operation makes the counter update indivisible. Relaxed ordering is enough only when no other data is published through this counter and final reading occurs after the join.

## Complete example

```c
#include <stdatomic.h>
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

struct Work {
    atomic_int *counter;
    int repetitions;
};

static int increment(void *argument)
{
    const struct Work *work = argument;
    for (int index = 0; index < work->repetitions; ++index) {
        (void)atomic_fetch_add_explicit(
            work->counter, 1, memory_order_relaxed);
    }
    return 0;
}

int main(void)
{
    atomic_int counter = ATOMIC_VAR_INIT(0);
    const struct Work work = {.counter = &counter, .repetitions = 5000};
    thrd_t worker;

    if (thrd_create(&worker, increment, (void *)&work) != thrd_success) {
        return EXIT_FAILURE;
    }
    (void)increment((void *)&work);

    int result = 0;
    if (thrd_join(worker, &result) != thrd_success || result != 0) {
        return EXIT_FAILURE;
    }

    printf("%d\n", atomic_load_explicit(
        &counter, memory_order_relaxed));
    return EXIT_SUCCESS;
}
```

Build and run:

```text
A C17 implementation with threads.h:
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
./main
```

Expected result:

```text
10000
```

## Common mistake

If resource acquisition partially succeeds, cleanup must still cover the resources already acquired.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only afterward.

Continue to [Module 30](../30-networking-and-platform-boundaries/README.md).
