# Module 35: Package and Release C Programs

## What you will learn

This lesson adds one clearly bounded systems skill to the C17 foundation.

## A release needs identity

Use a deliberate version, source revision, release notes, and license. Version output connects a bug report with a specific artifact.

## Instructions must reproduce the build

Document platforms, compilers, C baseline, dependencies, configure, build, test, install, run, and removal steps.

## Test the package itself

Create an archive from intended inputs, unpack it into an empty directory, follow the published steps, inspect dependencies, and verify checksums and contents.

## Complete example

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#ifndef APP_VERSION
#define APP_VERSION "0.1.0"
#endif

int main(int argument_count, char *arguments[])
{
    if (argument_count == 1) {
        puts("sample application");
        return EXIT_SUCCESS;
    }
    if (argument_count == 2 &&
        strcmp(arguments[1], "--version") == 0) {
        puts(APP_VERSION);
        return EXIT_SUCCESS;
    }

    fprintf(stderr, "Usage: %s [--version]\n", arguments[0]);
    return EXIT_FAILURE;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o sample
./sample --version
```

Expected result:

```text
0.1.0
```

## Common mistake

A binary copied from a developer directory is not a reproducible release without source identity, build settings, dependencies, instructions, and license material.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only after trying.

