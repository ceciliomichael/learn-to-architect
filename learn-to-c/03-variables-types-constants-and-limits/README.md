# Module 03: Variables, Types, Constants, and Limits

## What you will learn

You will choose types by meaning, initialize every value, and ask the implementation for its limits instead of guessing.

## A type defines valid operations

An int is useful for ordinary whole-number arithmetic. A double represents an approximate real number. A size_t represents object sizes and array counts. Fixed-width integer types are useful when an external format requires an exact width.

## Initialize before reading

An automatic local variable has an indeterminate value until you store one. Reading it is not a harmless default. Declare a variable close to its first useful value.

## Constants protect intent

const prevents later assignment through that name. Headers such as limits.h and stdint.h describe ranges supplied by the implementation.

## Complete example

```c
#include <inttypes.h>
#include <limits.h>
#include <stddef.h>
#include <stdint.h>
#include <stdio.h>

int main(void)
{
    const int passing_score = 70;
    const size_t learner_count = 3U;
    const int32_t balance_cents = 1250;

    printf("passing score: %d\n", passing_score);
    printf("learners: %zu\n", learner_count);
    printf("balance: %" PRId32 " cents\n", balance_cents);
    printf("largest int: %d\n", INT_MAX);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
Four labeled lines. The final number depends on the implementation's int range.
```

## Common mistake

Do not print size_t or fixed-width integers with a guessed format. Use %zu for size_t and the macros from inttypes.h for fixed-width types.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 04](../04-operators-conversions-and-overflow/README.md).

