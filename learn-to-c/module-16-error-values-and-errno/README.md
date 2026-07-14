# Module 16: Error Values and errno

## What you will learn

You will parse text without confusing a valid value with failure and use errno only where a function's contract gives it meaning.

## Return values come first

Many C functions report success or failure through their return value and provide data through another result. Read that function's documented contract rather than assuming zero or NULL always means the same thing.

## errno is not a universal last error

A function documents whether it may set errno. Set errno to zero before calls such as strtol when you need to distinguish range failure, then inspect it only after that call reports a relevant result.

## Parsing needs a complete-consumption rule

strtol reports where conversion stopped. Reject no digits, overflow, values outside the destination type, and unexpected trailing characters. Whitespace policy should be explicit.

## Complete example

```c
#include <ctype.h>
#include <errno.h>
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>

static int parse_int(const char *text, int *result)
{
    char *end = NULL;
    errno = 0;
    const long value = strtol(text, &end, 10);

    if (end == text || errno == ERANGE || value < INT_MIN || value > INT_MAX) {
        return 0;
    }
    while (isspace((unsigned char)*end) != 0) {
        ++end;
    }
    if (*end != '\0') {
        return 0;
    }

    *result = (int)value;
    return 1;
}

int main(void)
{
    int value = 0;
    if (parse_int(" 2048 ", &value) == 0) {
        fputs("Invalid integer.\n", stderr);
        return EXIT_FAILURE;
    }

    printf("%d\n", value);
    return EXIT_SUCCESS;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
2048
```

## Common mistake

atoi cannot distinguish invalid input from a valid zero and does not provide a useful overflow contract. Prefer a checked conversion such as strtol.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 17](../module-17-files-and-streams/README.md).

