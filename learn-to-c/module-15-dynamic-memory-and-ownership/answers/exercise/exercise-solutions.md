# Exercise Solution: Dynamic Memory and Ownership

```c
#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    const size_t count = 4U;
    if (count > SIZE_MAX / sizeof(double)) {
        fputs("Requested size is too large.\n", stderr);
        return EXIT_FAILURE;
    }

    double *values = malloc(count * sizeof *values);
    if (values == NULL) {
        fputs("Allocation failed.\n", stderr);
        return EXIT_FAILURE;
    }

    values[0] = 1.5;
    values[1] = 2.5;
    values[2] = 3.5;
    values[3] = 4.5;

    double total = 0.0;
    for (size_t index = 0U; index < count; ++index) {
        total += values[index];
    }

    printf("%.1f\n", total);
    free(values);
    return EXIT_SUCCESS;
}
```

## Why this solution works

The requested byte count is proven representable, allocation failure is handled, ownership is released once, and the total is 12.0. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

