# Module 02: Preprocess, Compile, Link, and Run

## What you will learn

You will separate the four jobs hidden inside a normal build command. This makes later errors much easier to locate.

## The preprocessor handles directives

Before C syntax is compiled, lines beginning with # are processed. An include directive makes declarations from a header available to this source file.

## Compilation creates object code

The compiler checks types and expressions, then produces an object file. An object file contains machine code but may still refer to functions supplied elsewhere.

## The linker finishes the program

The linker combines object files and libraries, resolves referenced names, and writes the executable. Running is a separate step performed only after a successful link.

## Complete example

```c
#include <stdio.h>

static int doubled(int value)
{
    return value * 2;
}

int main(void)
{
    printf("%d\n", doubled(21));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow -c main.c -o main.o
gcc main.o -o main
./main
```

Expected result:

```text
42
```

## Common mistake

A declaration error is usually a compile problem. An undefined reference after successful compilation is usually a link problem. The stage named by the diagnostic matters.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 03](../03-variables-types-constants-and-limits/README.md).

