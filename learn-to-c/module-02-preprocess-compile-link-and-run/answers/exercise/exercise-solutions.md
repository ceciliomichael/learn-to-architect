# Exercise Solution: Preprocess, Compile, Link, and Run

```c
#include <stdio.h>

static int tripled(int value)
{
    return value * 3;
}

int main(void)
{
    printf("%d\n", tripled(21));
    return 0;
}
```

## Why this solution works

The separate compile and link commands succeed, and the executable prints 63. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

