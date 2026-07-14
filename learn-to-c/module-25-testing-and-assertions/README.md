# Module 25: Testing and Assertions

## What you will learn

This module builds the next production C skill without hiding its contracts.

## Tests make requirements repeatable

Keep calculations separate from I/O so tests can call them directly. Check ordinary cases, boundaries, and each invalid case promised by the contract.

## Assertions are for programmer errors

assert is suitable for an invariant that must hold when the program is correct. It can be disabled with NDEBUG, so never use it to perform required work or as the only validation for external input.

## Use more than one build

Run tests with strict warnings, sanitizers where supported, and an optimized build. Each configuration provides different evidence.

## Complete example

```c
#include <assert.h>
#include <stdio.h>

static int clamp(int value, int minimum, int maximum)
{
    assert(minimum <= maximum);
    if (value < minimum) {
        return minimum;
    }
    if (value > maximum) {
        return maximum;
    }
    return value;
}

int main(void)
{
    assert(clamp(-1, 0, 10) == 0);
    assert(clamp(4, 0, 10) == 4);
    assert(clamp(15, 0, 10) == 10);
    puts("all tests passed");
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o tests
./tests
```

Expected result:

```text
all tests passed
```

## Common mistake

Do not write assert(read_record(file)). When assertions are disabled, the required read call disappears.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only afterward.

Continue to [Module 26](../module-26-debuggers-sanitizers-and-static-analysis/README.md).

