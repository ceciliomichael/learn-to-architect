# Exercise Solution: Conditions and Switch

```c
#include <stdio.h>

int main(void)
{
    const int month = 2;

    if (month < 1 || month > 12) {
        puts("Invalid month");
    } else {
        switch (month) {
            case 1:
            case 2:
            case 3:
                puts("First quarter");
                break;
            default:
                puts("Later quarter");
                break;
        }
    }
    return 0;
}
```

## Why this solution works

Values outside 1 through 12 are rejected, 1 through 3 select the first quarter, and all other valid values select the later-quarter path. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

