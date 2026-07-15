# Exercise Solution: Files and Streams

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    const char path[] = "exercise-data.txt";
    FILE *file = fopen(path, "w");
    if (file == NULL) {
        perror("open for writing");
        return EXIT_FAILURE;
    }

    if (fprintf(file, "first: %d\nsecond: %d\n", 7, 11) < 0) {
        fputs("write failed\n", stderr);
        (void)fclose(file);
        return EXIT_FAILURE;
    }
    if (fclose(file) != 0) {
        fputs("close after writing failed\n", stderr);
        return EXIT_FAILURE;
    }

    file = fopen(path, "r");
    if (file == NULL) {
        perror("open for reading");
        return EXIT_FAILURE;
    }

    char line[64] = "";
    while (fgets(line, sizeof line, file) != NULL) {
        fputs(line, stdout);
    }
    if (ferror(file) != 0) {
        fputs("read failed\n", stderr);
        (void)fclose(file);
        return EXIT_FAILURE;
    }
    if (fclose(file) != 0) {
        fputs("close after reading failed\n", stderr);
        return EXIT_FAILURE;
    }
    return EXIT_SUCCESS;
}
```

## Why this solution works

The program verifies each file boundary, prints both stored lines, and closes each successfully opened stream exactly once. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

