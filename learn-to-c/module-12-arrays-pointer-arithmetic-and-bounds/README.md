# Module 12: Arrays, Pointer Arithmetic, and Bounds

## What you will learn

You will connect array indexing with pointer movement while keeping every pointer within one array object.

## Array elements are contiguous

In most expressions, an array name is converted to a pointer to its first element. Adding one to an int pointer advances by one int element, not one byte.

## One-past is a boundary, not an element

A pointer may be formed one past the final array element for comparison and loop termination. It must not be dereferenced. Pointer ordering and subtraction are meaningful only within the same array object.

## Prefer the clearest notation

values[index] and *(values + index) designate the same valid element. Indexing is often easier to audit. Pointer iteration is useful when the begin and end boundary stay together.

## Complete example

```c
#include <stddef.h>
#include <stdio.h>

static int sum(const int *begin, const int *end)
{
    int total = 0;
    for (const int *current = begin; current < end; ++current) {
        total += *current;
    }
    return total;
}

int main(void)
{
    const int values[] = {3, 6, 9, 12};
    const size_t count = sizeof values / sizeof values[0];

    printf("%d\n", sum(values, values + count));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
30
```

## Common mistake

values + count is a useful one-past pointer, but *(values + count) is outside the array and has undefined behavior.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 13](../module-13-structures-and-data-ownership/README.md).

