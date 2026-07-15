# Exercise Solution: Function Pointers and Callbacks

```c
#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>

static int compare_descending(const void *left_value, const void *right_value)
{
    const int left = *(const int *)left_value;
    const int right = *(const int *)right_value;
    return (left < right) - (left > right);
}

int main(void)
{
    int values[] = {5, 1, 8, 3};
    const size_t count = sizeof values / sizeof values[0];

    qsort(values, count, sizeof values[0], compare_descending);
    for (size_t index = 0U; index < count; ++index) {
        printf("%d%s", values[index], index + 1U == count ? "\n" : " ");
    }
    return 0;
}
```

## Why this solution works

The callback exactly matches qsort's type, avoids overflowing subtraction, and produces 8 5 3 1. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

