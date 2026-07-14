# Module 17: Files and Streams

## What you will learn

You will open a file, check every I/O boundary, close it, and separate stored data from an in-memory value.

## A FILE pointer represents a stream

fopen returns a stream or NULL. The mode controls reading, writing, appending, and whether text translation may occur. Use binary modes when exact bytes matter.

## I/O can fail after opening

A successful fopen does not guarantee later writes, flushes, or closes will succeed. Check the operation that establishes each important result.

## Cleanup follows ownership

The code that successfully opens a stream normally owns the matching fclose. Keep cleanup paths simple so that every acquired resource is released once.

## Complete example

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    const char path[] = "lesson-note.txt";
    FILE *output = fopen(path, "w");
    if (output == NULL) {
        perror("Could not open output");
        return EXIT_FAILURE;
    }

    if (fprintf(output, "careful file handling\n") < 0) {
        fputs("Could not write the note.\n", stderr);
        (void)fclose(output);
        return EXIT_FAILURE;
    }
    if (fclose(output) != 0) {
        fputs("Could not finish the file.\n", stderr);
        return EXIT_FAILURE;
    }

    FILE *input = fopen(path, "r");
    if (input == NULL) {
        perror("Could not open input");
        return EXIT_FAILURE;
    }

    char line[64] = "";
    if (fgets(line, sizeof line, input) == NULL) {
        fputs("Could not read the note.\n", stderr);
        (void)fclose(input);
        return EXIT_FAILURE;
    }

    fputs(line, stdout);
    if (fclose(input) != 0) {
        fputs("Could not close input.\n", stderr);
        return EXIT_FAILURE;
    }
    return EXIT_SUCCESS;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
careful file handling
```

## Common mistake

feof does not predict whether the next read will succeed. Attempt the read, inspect its return value, then use feof and ferror only when you need to classify the failure.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 18](../module-18-preprocessor-includes-macros-and-generic-selection/README.md).

