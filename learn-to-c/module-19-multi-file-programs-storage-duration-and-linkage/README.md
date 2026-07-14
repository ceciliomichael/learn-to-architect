# Module 19: Multi-File Programs, Storage Duration, and Linkage

## What you will learn

You will split an interface from its implementation and understand which names are shared across translation units.

## Each source file is compiled separately

After preprocessing, one source file becomes one translation unit. A header supplies consistent declarations, while exactly one source file normally supplies each external definition.

## Linkage controls name identity

A file-level function or object has external linkage by default unless static gives it internal linkage. Internal helpers cannot collide with same-named helpers in another source file.

## Storage duration controls lifetime

Automatic local objects normally live for one block execution. Static-duration objects exist for the program's entire run. Linkage and lifetime answer different questions.

## Complete example

Create these three files.

```c
/* arithmetic.h */
#ifndef ARITHMETIC_H
#define ARITHMETIC_H

int add(int left, int right);

#endif
```

```c
/* arithmetic.c */
#include "arithmetic.h"

static int normalize(int value)
{
    return value;
}

int add(int left, int right)
{
    return normalize(left) + normalize(right);
}
```

```c
/* main.c */
#include "arithmetic.h"
#include <stdio.h>

int main(void)
{
    printf("%d\n", add(20, 22));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow -c arithmetic.c
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow -c main.c
gcc arithmetic.o main.o -o main
./main
```

Expected result:

```text
42
```

## Common mistake

Do not put an ordinary external function definition in a header included by several source files. The linker will see several definitions of the same name.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 20](../module-20-function-pointers-and-callbacks/README.md).

