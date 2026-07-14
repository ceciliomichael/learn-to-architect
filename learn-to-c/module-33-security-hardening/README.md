# Module 33: Security Hardening

## What you will learn

This lesson adds one clearly bounded systems skill to the C17 foundation.

## Treat boundaries as hostile

Validate command lines, environment data, files, networks, and foreign calls for length, syntax, range, and policy before use.

## Memory safety begins in design

Carry capacities and verified lengths, check size arithmetic, centralize ownership, and reject excess input instead of silently using a prefix.

## Hardening is an extra layer

Warnings, sanitizers, stack protection, fortified calls, control-flow defenses, non-executable memory, and randomization cover different risks. Exact support is platform-specific.

## Complete example

```c
#include <limits.h>
#include <stdio.h>
#include <string.h>

static int read_complete_line(char buffer[], size_t capacity)
{
    if (buffer == NULL || capacity < 2U ||
        capacity > (size_t)INT_MAX) {
        return 0;
    }
    if (fgets(buffer, (int)capacity, stdin) == NULL) {
        return 0;
    }

    char *newline = strchr(buffer, '\n');
    if (newline != NULL) {
        *newline = '\0';
        return 1;
    }
    if (feof(stdin) != 0) {
        return 1;
    }

    int character = 0;
    do {
        character = fgetc(stdin);
    } while (character != '\n' && character != EOF);

    buffer[0] = '\0';
    return 0;
}

int main(void)
{
    char name[32] = "";
    if (read_complete_line(name, sizeof name) == 0) {
        fputs("Name is missing or too long.\n", stderr);
        return 1;
    }
    printf("Accepted: %s\n", name);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
A complete bounded line is accepted. An overlong line is drained and rejected.
```

## Common mistake

Silent truncation can make validation apply to a different identifier, path, or command than the sender supplied.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only after trying.

Continue to [Module 34](../module-34-portability-standards-and-c23/README.md).

