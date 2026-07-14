# Module 14: Enumerations, typedef, and Flags

## What you will learn

You will name a closed set of choices, introduce readable type aliases, and combine independent options with bit masks.

## An enumeration names integral constants

enum values are useful for states and choices. A variable can still contain an unlisted integer, so validate values received from files, networks, or casts.

## A typedef aliases a type

typedef can shorten a deliberate public type name. It does not create runtime data and should not hide whether a type has pointer semantics.

## Flags need independent bits

A flag mask uses one bit per option. Combine flags with bitwise OR, test with bitwise AND, and remove with AND plus complement. Use an unsigned mask to make bit behavior clearer.

## Complete example

```c
#include <stdbool.h>
#include <stdio.h>

typedef enum {
    STATUS_PENDING,
    STATUS_READY,
    STATUS_FAILED
} Status;

enum Permission {
    PERMISSION_READ = 1U << 0,
    PERMISSION_WRITE = 1U << 1
};

static bool has_permission(unsigned permissions, unsigned required)
{
    return (permissions & required) == required;
}

int main(void)
{
    const Status status = STATUS_READY;
    const unsigned permissions = PERMISSION_READ | PERMISSION_WRITE;

    printf("ready: %s\n", status == STATUS_READY ? "yes" : "no");
    printf("can write: %s\n",
           has_permission(permissions, PERMISSION_WRITE) ? "yes" : "no");
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
ready: yes
can write: yes
```

## Common mistake

Logical OR uses || and produces a truth value. Bitwise OR uses | and combines flag bits. They are not interchangeable.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 15](../module-15-dynamic-memory-and-ownership/README.md).

