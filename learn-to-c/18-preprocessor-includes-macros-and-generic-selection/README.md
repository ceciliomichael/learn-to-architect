# Module 18: Preprocessor, Includes, Macros, and Generic Selection

## What you will learn

You will use headers and conditional compilation carefully, write narrow macros, and understand that macro replacement happens before type checking.

## Headers share declarations

A header should expose declarations needed by more than one source file. Include guards prevent repeated inclusion within one preprocessing translation.

## Macros replace tokens

A function-like macro is not an ordinary function. Parenthesize parameters and the complete expression, and do not evaluate an argument more times than the macro documents.

## Generic selection chooses by type

The C11 _Generic expression selects an expression based on the controlling expression's type. It can build small type-aware interfaces, but every selected branch still needs valid source.

## Complete example

```c
#include <stddef.h>
#include <stdio.h>

#define ARRAY_COUNT(array) (sizeof(array) / sizeof((array)[0]))
#define TYPE_NAME(value) \
    _Generic((value), int: "int", double: "double", default: "other")

int main(void)
{
    const int values[] = {2, 4, 6};

    printf("count: %zu\n", ARRAY_COUNT(values));
    printf("type: %s\n", TYPE_NAME(values[0]));
    printf("type: %s\n", TYPE_NAME(2.5));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
count: 3
type: int
type: double
```

## Common mistake

ARRAY_COUNT works for an actual array, not a pointer. With a pointer it divides two unrelated object sizes and may produce a plausible but wrong count.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 19](../19-multi-file-programs-storage-duration-and-linkage/README.md).

