# Module 15: Dynamic Memory and Ownership

## What you will learn

You will allocate storage whose size is known at runtime, check every size calculation, and release exactly the allocation you own.

## Allocation returns storage or failure

malloc returns a suitably aligned block or NULL. In C, do not cast its void pointer result. A cast can hide a missing stdlib.h declaration.

## Check multiplication before allocating

count * sizeof element can wrap in size_t before malloc sees it. Establish count <= SIZE_MAX / sizeof element and apply a sensible maximum for external sizes.

## One owner releases once

A successful allocation must eventually be passed to free exactly once. After free, every pointer to that object is invalid to dereference. Setting one local pointer to NULL does not repair other aliases.

## Complete example

```c
#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    const size_t count = 5U;

    if (count > SIZE_MAX / sizeof(int)) {
        fputs("Requested size is too large.\n", stderr);
        return EXIT_FAILURE;
    }

    int *values = malloc(count * sizeof *values);
    if (values == NULL) {
        fputs("Allocation failed.\n", stderr);
        return EXIT_FAILURE;
    }

    for (size_t index = 0U; index < count; ++index) {
        values[index] = (int)(index + 1U);
    }

    printf("last: %d\n", values[count - 1U]);
    free(values);
    return EXIT_SUCCESS;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
last: 5
```

## Common mistake

Do not multiply untrusted count by an element size and then check the product. If multiplication wrapped, the original required size has already been lost.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 16](../16-error-values-and-errno/README.md).

