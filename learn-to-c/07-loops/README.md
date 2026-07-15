# Module 07: Loops

## What you will learn

You will repeat work with a visible stopping condition and avoid common off-by-one errors.

## Choose the loop that states the job

A for loop is helpful when initialization, condition, and update belong together. A while loop is useful when repetition depends on a condition produced elsewhere. A do loop always runs its body at least once.

## Establish progress

A loop must either reach its stopping condition or be intentionally infinite. Write down which value changes and why that change eventually stops the loop.

## Keep boundaries exact

For a count of five items, indexes normally run from 0 through 4. The comparison index < count expresses that half-open range directly.

## Complete example

```c
#include <stddef.h>
#include <stdio.h>

int main(void)
{
    const size_t count = 5U;
    int total = 0;

    for (size_t index = 0U; index < count; ++index) {
        total += (int)(index + 1U);
    }

    printf("total: %d\n", total);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
total: 15
```

## Common mistake

Using index <= count performs one extra iteration. When index names an array position, that mistake can access outside the array.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 08](../08-functions-scope-and-header-declarations/README.md).

