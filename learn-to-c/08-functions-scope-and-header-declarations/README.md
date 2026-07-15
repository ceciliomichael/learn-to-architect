# Module 08: Functions, Scope, and Header Declarations

## What you will learn

You will give a small calculation a name, state its input and output types, and understand where names are visible.

## A declaration states the callable contract

A function declaration tells the compiler its name, parameter types, and return type. A definition supplies the body. Place a declaration before the first call or use a header when several source files share it.

## Parameters are local values

C passes each argument by value. A parameter is a local copy, so changing it does not change the caller's variable. Pointer parameters, taught later, can provide access to caller-owned objects.

## Scope limits where a name can be used

A block scope begins at a declaration and ends at the closing brace. Small scopes reduce accidental reuse. static on a file-level helper keeps its name private to that source file.

## Complete example

```c
#include <stdio.h>

static int clamp(int value, int minimum, int maximum);

int main(void)
{
    const int safe_score = clamp(115, 0, 100);
    printf("%d\n", safe_score);
    return 0;
}

static int clamp(int value, int minimum, int maximum)
{
    if (value < minimum) {
        return minimum;
    }
    if (value > maximum) {
        return maximum;
    }
    return value;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
100
```

## Common mistake

Calling a function without a visible declaration is not a shortcut. Modern C requires the compiler to know the function contract before the call.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 09](../09-arrays-and-length-tracking/README.md).

