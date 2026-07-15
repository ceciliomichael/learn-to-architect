# Module 32: Measure and Improve Performance

## What you will learn

This lesson adds one clearly bounded systems skill to the C17 foundation.

## Measure a representative workload

Record inputs, compiler, options, hardware, and the output that must remain correct. An unrealistic micro-test can reward the wrong change.

## Use repeated observations

ISO clock reports processor time in implementation-defined units. Platform monotonic clocks or benchmark frameworks may better fit elapsed time. One timing is never enough.

## Optimize measured causes

Profile first. Consider algorithm, data layout, allocation, and I/O before tiny expression changes. Rerun correctness tests after every optimization.

## Complete example

```c
#include <inttypes.h>
#include <stdint.h>
#include <stdio.h>
#include <time.h>

int main(void)
{
    const uint32_t count = UINT32_C(5000000);
    uint64_t total = UINT64_C(0);
    const clock_t started = clock();

    for (uint32_t value = 0U; value < count; ++value) {
        total += value;
    }

    const clock_t finished = clock();
    if (started == (clock_t)-1 || finished == (clock_t)-1) {
        return 1;
    }

    const double seconds =
        (double)(finished - started) / (double)CLOCKS_PER_SEC;
    printf("total: %" PRIu64 "\n", total);
    printf("processor seconds: %.6f\n", seconds);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -O2 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
./main
```

Expected result:

```text
The total is 12499997500000. Time varies by run.
```

## Common mistake

If a computed result cannot affect observable behavior, the optimizer may remove the work you intended to measure.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only after trying.

Continue to [Module 33](../33-security-hardening/README.md).

