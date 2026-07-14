# Module 09: Arrays and Length Tracking

## What you will learn

You will store several values contiguously and carry the element count wherever it is needed.

## An array has a fixed number of elements

The declaration int scores[4] reserves four int objects. Their valid indexes are 0, 1, 2, and 3. C performs no automatic bounds check.

## Length is part of the contract

When an array is passed to a function, the parameter does not retain the array's length. Pass the count separately. Compute a local array's count with sizeof array / sizeof array[0] only where the name still denotes the actual array.

## Use size_t for sizes and indexes

size_t is the type produced by sizeof. A loop using size_t avoids converting between unrelated signed and unsigned types when it compares with a count.

## Complete example

```c
#include <stddef.h>
#include <stdio.h>

static int sum_scores(const int scores[], size_t count)
{
    int total = 0;
    for (size_t index = 0U; index < count; ++index) {
        total += scores[index];
    }
    return total;
}

int main(void)
{
    const int scores[] = {82, 91, 76, 88};
    const size_t count = sizeof scores / sizeof scores[0];

    printf("count: %zu\n", count);
    printf("total: %d\n", sum_scores(scores, count));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
count: 4
total: 337
```

## Common mistake

sizeof on an array parameter does not recover the caller's array length. In that function, the parameter is adjusted to a pointer.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 10](../module-10-characters-strings-and-bytes/README.md).

