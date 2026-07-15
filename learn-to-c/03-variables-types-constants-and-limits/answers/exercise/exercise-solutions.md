# Exercise Solution: Variables, Types, Constants, and Limits

```c
#include <limits.h>
#include <stddef.h>
#include <stdio.h>

int main(void)
{
    const int room_number = 204;
    const size_t item_count = 8U;
    const double temperature_c = 26.5;

    printf("room: %d\n", room_number);
    printf("items: %zu\n", item_count);
    printf("temperature: %.1f C\n", temperature_c);
    printf("smallest int: %d\n", INT_MIN);
    return 0;
}
```

## Why this solution works

All values are initialized, every format matches its argument, and the strict build has no warnings. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

