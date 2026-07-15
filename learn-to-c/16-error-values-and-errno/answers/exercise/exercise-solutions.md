# Exercise Solution: Error Values and errno

```c
#include <ctype.h>
#include <errno.h>
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>

static int parse_int(const char *text, int *result)
{
    if (text == NULL || result == NULL) {
        return 0;
    }

    char *end = NULL;
    errno = 0;
    const long value = strtol(text, &end, 10);
    if (end == text || errno == ERANGE || value < INT_MIN || value > INT_MAX) {
        return 0;
    }

    while (isspace((unsigned char)*end) != 0) {
        ++end;
    }
    if (*end != '\0') {
        return 0;
    }

    *result = (int)value;
    return 1;
}

int main(void)
{
    int value = 0;
    if (parse_int(" -17 ", &value) == 0) {
        fputs("Invalid integer.\n", stderr);
        return EXIT_FAILURE;
    }

    printf("%d\n", value);
    return EXIT_SUCCESS;
}
```

## Why this solution works

The parser accepts the complete valid value, rejects partial and out-of-range text, and writes the result only on success. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

