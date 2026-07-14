# Module 26: Debuggers, Sanitizers, and Static Analysis

## What you will learn

This module builds the next production C skill without hiding its contracts.

## A debugger explains one run

Build with debug information, pause at breakpoints, step through source, and inspect variables and the call stack.

## Sanitizers add runtime checks

AddressSanitizer and UndefinedBehaviorSanitizer detect many memory and language violations on executed paths. Platform and compiler support varies.

## Static analysis explores possible paths

Compiler analyzers can find suspicious ownership, control flow, and API use without executing every path. Understand a diagnostic before changing code.

## Complete example

```c
#include <stddef.h>
#include <stdint.h>
#include <stdio.h>

static size_t find_index(const int values[], size_t count, int wanted)
{
    for (size_t index = 0U; index < count; ++index) {
        if (values[index] == wanted) {
            return index;
        }
    }
    return SIZE_MAX;
}

int main(void)
{
    const int values[] = {10, 20, 30};
    const size_t count = sizeof values / sizeof values[0];
    const size_t found = find_index(values, count, 20);

    if (found == SIZE_MAX) {
        puts("not found");
    } else {
        printf("found at %zu\n", found);
    }
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -g -O1 -Wall -Wextra -Wpedantic -Wconversion -Wshadow -fsanitize=address,undefined main.c -o main
./main
```

Expected result:

```text
found at 1
```

## Common mistake

A clean sanitizer run covers only the paths that ran and only the defect classes that sanitizer supports.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only afterward.

Continue to [Module 27](../module-27-make-and-repeatable-builds/README.md).

