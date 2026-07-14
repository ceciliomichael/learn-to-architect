# Module 34: Portability, Standards, and C23

## What you will learn

This lesson adds one clearly bounded systems skill to the C17 foundation.

## Compiler and language versions differ

A new compiler can support several C editions. Select the standard explicitly and inspect __STDC_VERSION__ instead of relying on the compiler default.

## Portability has several layers

Widths, char signedness, byte order, alignment, libraries, operating systems, and build tools may differ. Standard code and isolated platform adapters address different layers.

## Adopt C23 deliberately

C23 features arrive across compilers and libraries at different times. Raise the baseline only when all supported environments supply the required features.

## Complete example

```c
#include <stdio.h>

int main(void)
{
#if defined(__STDC_VERSION__)
    printf("__STDC_VERSION__: %ld\n", __STDC_VERSION__);
#else
    puts("No standard version value.");
#endif

#if defined(__STDC_VERSION__) && __STDC_VERSION__ >= 202311L
    puts("C23 or later language mode");
#else
    puts("Earlier than C23 language mode");
#endif
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o c17-app
gcc -std=c23 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o c23-app
```

Expected result:

```text
C17 reports 201710 and the earlier branch. A conforming C23 mode reports at least 202311.
```

## Common mistake

A compiler brand check is weaker than a direct test for the language or library feature the program needs.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only after trying.

Continue to [Module 35](../module-35-package-and-release/README.md).

