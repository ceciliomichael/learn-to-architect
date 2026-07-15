# Module 10: Characters, Strings, and Bytes

## What you will learn

You will distinguish one character, a terminated C string, and an arbitrary byte buffer.

## A C string needs a terminator

A string is a sequence of char values ending with a zero byte written as '\0'. An array of bytes is not automatically a string. String functions require a terminator within the accessible object.

## Capacity and length are different

Capacity is the array's total storage. strlen counts characters before the first terminator and does not include it. A destination must have room for content plus the terminator.

## Use bounded formatting

snprintf receives a destination capacity and reports how many characters it wanted to write. A nonnegative result greater than or equal to the capacity means truncation occurred.

## Complete example

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    const char given[] = "Ada";
    const char family[] = "Lovelace";
    char full_name[32] = "";

    const int written =
        snprintf(full_name, sizeof full_name, "%s %s", given, family);
    if (written < 0 || (size_t)written >= sizeof full_name) {
        fputs("Name did not fit.\n", stderr);
        return 1;
    }

    printf("%s has %zu characters.\n", full_name, strlen(full_name));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
Ada Lovelace has 12 characters.
```

## Common mistake

Do not call strlen on raw bytes unless a zero terminator is known to occur within the buffer. strlen keeps reading until it finds one.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 11](../11-pointers-addresses-and-null/README.md).

