# Exercise Solution: Loops

```c
#include <stdio.h>

int main(void)
{
    for (int value = 1; value <= 5; ++value) {
        printf("%d\n", value);
    }

    int remaining = 3;
    while (remaining > 0) {
        printf("%d\n", remaining);
        --remaining;
    }

    puts("Go");
    return 0;
}
```

## Why this solution works

The output contains 1 through 5, then 3 through 1, then Go, and both loops visibly move toward their stopping condition. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

