# Module 01: Online Compiler and Local Toolchain Choices

## What you will learn

You will run a first C program and learn what a browser compiler can and cannot tell you. The goal is confidence with the edit, compile, run cycle, not memorizing every line.

## Start with a small program

A C source file is plain text. The compiler checks that text and turns it into a program the computer can run. In the browser, open the Programiz C compiler, replace its example, and select Run.

## Know when to work locally

A browser is useful for short, single-file experiments. Local GCC or Clang is needed for dependable warning flags, several source files, installed libraries, debuggers, sanitizers, and operating-system features. Never paste private code or data into a public compiler.

## Read diagnostics calmly

A compiler diagnostic is evidence, not a score. Start with the first relevant error, compare the reported line with the working example, fix one issue, and compile again.

## Complete example

```c
#include <stdio.h>

int main(void)
{
    puts("I am learning C.");
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
I am learning C.
```

## Common mistake

Do not remove void from main just because an online example uses main(). In C, main(void) clearly states that this program accepts no parameters.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../02-preprocess-compile-link-and-run/README.md).

