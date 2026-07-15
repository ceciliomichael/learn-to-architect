# Module 23: Undefined, Unspecified, and Implementation-Defined Behavior

## What you will learn

You will distinguish three categories the C standard uses and stop treating one successful run as proof of portable behavior.

## Undefined behavior has no required result

Examples include signed overflow, out-of-bounds access, invalid shifts, use after free, and mismatched variadic formats. After undefined behavior, the standard places no requirements on the execution.

## Unspecified behavior allows choices

The implementation may choose among permitted possibilities without documenting which choice occurs. Function argument evaluation order is a common example, so do not make correctness depend on it.

## Implementation-defined behavior is documented

The implementation chooses a behavior and must document it, such as whether plain char is signed. Compiler options and target documentation are part of the program's build contract.

## Complete example

```c
#include <limits.h>
#include <stdio.h>

int main(void)
{
    const unsigned width = (unsigned)(sizeof(unsigned) * CHAR_BIT);
    const unsigned highest_bit = 1U << (width - 1U);

    printf("unsigned width: %u\n", width);
    printf("highest bit: %u\n", highest_bit);
    printf("plain char minimum: %d\n", CHAR_MIN);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
The values describe the selected implementation. The shift remains within the unsigned type's width.
```

## Common mistake

A debug build printing the expected value does not define undefined behavior. Optimization or a different surrounding expression may produce a different outcome.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 24](../24-defensive-input-size-arithmetic-and-allocation-limits/README.md).

