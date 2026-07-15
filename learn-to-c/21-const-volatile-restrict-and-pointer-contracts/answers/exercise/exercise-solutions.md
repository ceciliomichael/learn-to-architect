# Exercise Solution: const, volatile, restrict, and Pointer Contracts

```c
#include <stddef.h>
#include <stdio.h>

static void copy_values(size_t count,
                        const int *restrict source,
                        int *restrict destination)
{
    for (size_t index = 0U; index < count; ++index) {
        destination[index] = source[index];
    }
}

int main(void)
{
    const int source[] = {4, 8, 12};
    int destination[3] = {0, 0, 0};
    const size_t count = sizeof source / sizeof source[0];

    copy_values(count, source, destination);
    printf("%d %d %d\n",
           destination[0], destination[1], destination[2]);
    return 0;
}
```

## Why this solution works

The source is read-only through its parameter, the two arrays satisfy the restrict promise, and the copied output is 4 8 12. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

