# Module 20: Function Pointers and Callbacks

## What you will learn

You will pass behavior through a typed function pointer and write a comparator that obeys its library contract.

## A function pointer has a full type

Its return type and parameter types define which functions it can designate. A callback API states when the function is called and what each result means.

## Comparators define ordering

qsort expects a negative result for less than, zero for equal, and positive for greater than. The callback receives pointers to elements as const void *, so convert them to the correct element pointer type before reading.

## Avoid arithmetic overflow in comparisons

Returning left - right can overflow. Compare relationally and combine the truth results instead.

## Complete example

```c
#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>

static int compare_ints(const void *left_value, const void *right_value)
{
    const int left = *(const int *)left_value;
    const int right = *(const int *)right_value;
    return (left > right) - (left < right);
}

int main(void)
{
    int values[] = {9, 2, 7, 2};
    const size_t count = sizeof values / sizeof values[0];

    qsort(values, count, sizeof values[0], compare_ints);

    for (size_t index = 0U; index < count; ++index) {
        printf("%d%s", values[index], index + 1U == count ? "\n" : " ");
    }
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
2 2 7 9
```

## Common mistake

A callback with a forced incompatible cast is not type-safe. Its actual function type must match what the receiving API will call.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 21](../module-21-const-volatile-restrict-and-pointer-contracts/README.md).

