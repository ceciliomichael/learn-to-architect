# Module 06: Conditions and Switch

## What you will learn

You will choose one path based on data and keep every branch clear.

## Conditions use zero and nonzero

In C, zero is false and a nonzero scalar value is true. Comparisons such as score >= 70 produce 0 or 1. Prefer a direct comparison when it states the rule clearly.

## An if chain handles ranges

Use if, else if, and else when conditions describe ranges or unrelated tests. Order matters because only the first matching branch runs.

## A switch handles discrete integral values

switch is useful for exact integer, character, or enumeration cases. A case normally needs break to avoid continuing into the next case. Use default for unsupported values when that is part of the contract.

## Complete example

```c
#include <stdio.h>

int main(void)
{
    const int score = 84;
    char grade = 'F';

    if (score >= 90) {
        grade = 'A';
    } else if (score >= 80) {
        grade = 'B';
    } else if (score >= 70) {
        grade = 'C';
    }

    switch (grade) {
        case 'A':
        case 'B':
            puts("Strong result");
            break;
        case 'C':
            puts("Passing result");
            break;
        default:
            puts("Keep practicing");
            break;
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
Strong result
```

## Common mistake

Assignment uses = and comparison uses ==. Writing if (score = 70) changes score and tests the assigned value.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 07](../07-loops/README.md).

