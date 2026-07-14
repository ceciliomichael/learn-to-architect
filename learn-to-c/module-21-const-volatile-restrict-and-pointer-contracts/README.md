# Module 21: const, volatile, restrict, and Pointer Contracts

## What you will learn

You will read pointer qualifiers as promises about access and avoid treating volatile as a threading tool.

## const protects through one access path

A pointer to const permits reading but not modification through that pointer. It does not necessarily prove the object is immutable through every alias.

## volatile concerns observable accesses

volatile tells the implementation that accesses to an object are observable and should occur according to the abstract-machine rules. It is used for special cases such as signal-visible objects and some hardware mappings. It does not make compound operations atomic or synchronize threads.

## restrict is an aliasing promise

For a restricted pointer used during an execution, the programmer promises the accessed object is not also accessed through conflicting unrelated pointers. This can enable optimization, but violating the promise creates undefined behavior.

## Complete example

```c
#include <stddef.h>
#include <stdio.h>

static void scale(size_t count,
                  const double *restrict input,
                  double *restrict output,
                  double factor)
{
    for (size_t index = 0U; index < count; ++index) {
        output[index] = input[index] * factor;
    }
}

int main(void)
{
    const double input[] = {1.0, 2.0, 3.0};
    double output[3] = {0.0, 0.0, 0.0};
    const size_t count = sizeof input / sizeof input[0];

    scale(count, input, output, 2.5);
    printf("%.1f %.1f %.1f\n", output[0], output[1], output[2]);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
2.5 5.0 7.5
```

## Common mistake

Calling scale with overlapping input and output regions would break its restrict contract. A compiler is not required to detect that violation.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 22](../module-22-bits-masks-representation-alignment-and-endianness/README.md).

