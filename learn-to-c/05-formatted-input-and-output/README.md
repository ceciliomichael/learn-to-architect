# Module 05: Formatted Input and Output

## What you will learn

You will send text to standard output, receive one bounded line from standard input, and handle input failure explicitly.

## Programs use standard streams

stdin normally receives input, stdout normally carries ordinary results, and stderr carries diagnostics. They may point to a terminal, file, or another process.

## Formats are contracts

Each printf conversion must match the corresponding argument type. A mismatch is not a cosmetic error. Enable format warnings and prefer simple functions such as puts when no formatting is needed.

## Bound input by the destination

fgets receives the buffer size and stores at most one less character plus a terminating zero byte. It can fail, and a long line may not fit completely. Later modules develop complete parsers.

## Complete example

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char name[32] = "";

    fputs("Name: ", stdout);
    if (fgets(name, sizeof name, stdin) == NULL) {
        fputs("Could not read a name.\n", stderr);
        return EXIT_FAILURE;
    }

    printf("Hello, %s", name);
    return EXIT_SUCCESS;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
After a name is entered, the program prints Hello followed by that line.
```

## Common mistake

Do not use gets. It has no way to know the destination size and was removed from the C standard.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 06](../06-conditions-and-switch/README.md).

