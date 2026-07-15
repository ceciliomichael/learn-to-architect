# Exercise Solution: Debuggers, Sanitizers, and Static Analysis

```c
#include <assert.h>
#include <stddef.h>
#include <stdint.h>
#include <stdio.h>

static size_t find_index(const int values[], size_t count, int wanted)
{
    for (size_t index = 0U; index < count; ++index) {
        if (values[index] == wanted) {
            return index;
        }
    }
    return SIZE_MAX;
}

int main(void)
{
    const int values[] = {10, 20, 30};
    const size_t count = sizeof values / sizeof values[0];

    assert(find_index(values, count, 10) == 0U);
    assert(find_index(values, count, 30) == 2U);
    assert(find_index(values, count, 99) == SIZE_MAX);
    puts("diagnostic cases passed");
    return 0;
}
```

## Why it works

First, last, and missing paths run, strict warnings remain clean, and supported tools report no violation. The relevant inputs, boundaries, and failures remain visible.

