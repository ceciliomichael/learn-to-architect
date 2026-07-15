# Exercise Solution: Arrays, Pointer Arithmetic, and Bounds

```c
#include <stddef.h>
#include <stdio.h>

static size_t count_even(const int *begin, const int *end)
{
    size_t count = 0U;
    for (const int *current = begin; current < end; ++current) {
        if (*current % 2 == 0) {
            ++count;
        }
    }
    return count;
}

int main(void)
{
    const int values[] = {2, 4, 6, 8};
    const size_t count = sizeof values / sizeof values[0];

    printf("%zu\n", count_even(values, values + count));
    return 0;
}
```

## Why this solution works

The loop stops at the one-past boundary without dereferencing it and prints 4. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

