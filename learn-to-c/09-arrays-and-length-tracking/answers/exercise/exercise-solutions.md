# Exercise Solution: Arrays and Length Tracking

```c
#include <stddef.h>
#include <stdio.h>

static int maximum(const int values[], size_t count)
{
    int result = values[0];
    for (size_t index = 1U; index < count; ++index) {
        if (values[index] > result) {
            result = values[index];
        }
    }
    return result;
}

int main(void)
{
    const int values[] = {4, 7, 1, 9, 3};
    const size_t count = sizeof values / sizeof values[0];

    printf("count: %zu\n", count);
    printf("maximum: %d\n", maximum(values, count));
    return 0;
}
```

## Why this solution works

The function never uses an index equal to count, and the output reports 5 elements with a maximum of 9. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

