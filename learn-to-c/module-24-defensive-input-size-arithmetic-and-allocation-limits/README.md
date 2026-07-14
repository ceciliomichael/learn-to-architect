# Module 24: Defensive Input, Size Arithmetic, and Allocation Limits

## What you will learn

You will turn external text into a bounded size only after validating syntax, range, multiplication, and an application limit.

## Validate in stages

First validate the text conversion, then the destination type's range, then the application's policy. Keeping stages separate makes a rejection explainable.

## A representable request may still be unreasonable

SIZE_MAX is a language limit, not a safe application quota. Set a maximum count or byte budget based on the program's purpose and reject larger requests before allocating.

## Check every size operation

Addition and multiplication can wrap in size_t. Check before the operation. The resulting allocation still may fail and must be handled.

## Complete example

```c
#include <errno.h>
#include <inttypes.h>
#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

static int parse_count(const char *text, size_t maximum, size_t *result)
{
    char *end = NULL;
    errno = 0;
    const uintmax_t raw = strtoumax(text, &end, 10);

    if (end == text || *end != '\0' || errno == ERANGE ||
        raw > SIZE_MAX || raw > maximum) {
        return 0;
    }

    *result = (size_t)raw;
    return 1;
}

int main(void)
{
    size_t count = 0U;
    if (parse_count("250", 1000U, &count) == 0 ||
        count > SIZE_MAX / sizeof(int)) {
        fputs("Invalid count.\n", stderr);
        return EXIT_FAILURE;
    }

    int *values = malloc(count * sizeof *values);
    if (values == NULL && count != 0U) {
        fputs("Allocation failed.\n", stderr);
        return EXIT_FAILURE;
    }

    printf("accepted count: %zu\n", count);
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
accepted count: 250
```

## Common mistake

Rejecting only values greater than SIZE_MAX still permits requests that can exhaust memory or make the program unusably slow.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 25](../module-25-testing-and-assertions/README.md).

