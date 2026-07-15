# Module 04: Operators, Conversions, and Overflow

## What you will learn

You will make arithmetic conversions visible and avoid relying on signed overflow.

## Operators follow type rules

An expression is evaluated using the types of its operands. Integer division discards the fractional part. Parentheses can clarify grouping, but they do not change an operand's type.

## Conversions deserve attention

An implicit conversion can lose range, sign, or fractional information. Strong warning flags help, but a deliberate cast should explain a decision rather than silence a warning.

## Signed overflow is not wrapping arithmetic

If a signed integer result is outside its type's range, the behavior is undefined. Widen operands before the operation when the wider type can hold the result, and check limits when even the wider result could overflow.

## Complete example

```c
#include <inttypes.h>
#include <stdint.h>
#include <stdio.h>

int main(void)
{
    const int first = 1500000000;
    const int second = 1000000000;
    const int64_t total = (int64_t)first + (int64_t)second;
    const double average = (double)total / 2.0;

    printf("total: %" PRId64 "\n", total);
    printf("average: %.1f\n", average);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
total: 2500000000
average: 1250000000.0
```

## Common mistake

Casting after an overflowing operation is too late. In (int64_t)(first + second), the int addition happens before the conversion.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 05](../05-formatted-input-and-output/README.md).

