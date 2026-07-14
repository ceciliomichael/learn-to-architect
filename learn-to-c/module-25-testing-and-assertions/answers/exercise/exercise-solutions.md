# Exercise Solution: Testing and Assertions

```c
#include <assert.h>
#include <limits.h>
#include <stdio.h>

static int absolute_value(int value)
{
    assert(value != INT_MIN);
    return value < 0 ? -value : value;
}

int main(void)
{
    assert(absolute_value(-8) == 8);
    assert(absolute_value(0) == 0);
    assert(absolute_value(13) == 13);
    puts("tests passed");
    return 0;
}
```

## Why it works

Three behavior classes are checked, INT_MIN is an explicit programmer precondition, and success prints only after all checks. The relevant inputs, boundaries, and failures remain visible.

