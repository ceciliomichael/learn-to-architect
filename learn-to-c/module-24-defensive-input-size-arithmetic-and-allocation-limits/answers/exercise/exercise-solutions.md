# Exercise Solution: Defensive Input, Size Arithmetic, and Allocation Limits

```c
#include <errno.h>
#include <inttypes.h>
#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

static int parse_count(const char *text, size_t maximum, size_t *result)
{
    if (text == NULL || result == NULL) {
        return 0;
    }

    char *end = NULL;
    errno = 0;
    const uintmax_t raw = strtoumax(text, &end, 10);
    if (end == text || *end != '\0' || errno == ERANGE ||
        raw > SIZE_MAX || raw > maximum) {
        return 0;
    }

    *result = (size_t)raw;
    return 1;
}

int main(void)
{
    size_t count = 0U;
    if (parse_count("64", 128U, &count) == 0 ||
        count > SIZE_MAX / sizeof(double)) {
        fputs("Invalid count.\n", stderr);
        return EXIT_FAILURE;
    }

    double *values = malloc(count * sizeof *values);
    if (values == NULL && count != 0U) {
        fputs("Allocation failed.\n", stderr);
        return EXIT_FAILURE;
    }

    printf("accepted count: %zu\n", count);
    free(values);
    return EXIT_SUCCESS;
}
```

## Why this solution works

The syntax, type range, policy limit, multiplication, allocation result, and cleanup are all handled, and 64 is accepted. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

