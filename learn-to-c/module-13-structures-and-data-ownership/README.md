# Module 13: Structures and Data Ownership

## What you will learn

You will group related fields into one type and state whether each pointer field owns, borrows, or shares the data it names.

## A structure creates one record type

A struct groups fields that belong together. Each object has its own copy of non-pointer fields. Use the dot operator for a structure object and the arrow operator for a pointer to one.

## Copying is field by field

Assigning one structure value copies all fields. An embedded array is copied with the structure. A pointer field copies only an address, not the pointed-to object.

## Document ownership beside pointer fields

C does not record ownership in the type system. A pointer might borrow storage, own allocated storage, or refer to shared state. The surrounding API must state who keeps the object alive and who releases it.

## Complete example

```c
#include <stdio.h>

struct Reading {
    const char *label;
    double value;
};

static void print_reading(const struct Reading *reading)
{
    if (reading != NULL && reading->label != NULL) {
        printf("%s: %.1f\n", reading->label, reading->value);
    }
}

int main(void)
{
    const char temperature_label[] = "temperature";
    const struct Reading reading = {
        .label = temperature_label,
        .value = 26.5
    };

    print_reading(&reading);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
temperature: 26.5
```

## Common mistake

Copying reading copies the label pointer. It does not create another copy of the label text, so both records depend on the original text remaining alive.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 14](../module-14-enumerations-typedef-and-flags/README.md).

