# Module 31: Libraries, ABI Contracts, and Foreign Interfaces

## What you will learn

This lesson adds one clearly bounded systems skill to the C17 foundation.

## A public header is a source contract

It includes the standard types its declarations need and uses stable, documented names. An extern C guard supports C++ callers without changing C builds.

## An ABI is a binary contract

Calling convention, symbol naming, type sizes, structure layout, alignment, runtime libraries, and compiler options can affect compatibility.

## Ownership must cross the boundary

State who creates, borrows, mutates, and frees each object. Opaque handles keep private layout out of the ABI.

## Complete example

Build a static library and a separate client.

```c
/* arithmetic_api.h */
#ifndef ARITHMETIC_API_H
#define ARITHMETIC_API_H
#include <stdint.h>
#ifdef __cplusplus
extern "C" {
#endif
int32_t arithmetic_add(int32_t left, int32_t right);
#ifdef __cplusplus
}
#endif
#endif
```

```c
/* arithmetic_api.c */
#include "arithmetic_api.h"
int32_t arithmetic_add(int32_t left, int32_t right)
{
    return left + right;
}
```

```c
/* client.c */
#include "arithmetic_api.h"
#include <inttypes.h>
#include <stdio.h>
int main(void)
{
    printf("%" PRId32 "\n", arithmetic_add(19, 23));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow -c arithmetic_api.c
ar rcs libarithmetic.a arithmetic_api.o
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow client.c -L. -larithmetic -o client
```

Expected result:

```text
42
```

## Common mistake

Fixed-width value types do not freeze every ABI property, including calling convention and symbol visibility.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only after trying.

Continue to [Module 32](../32-measure-and-improve-performance/README.md).

