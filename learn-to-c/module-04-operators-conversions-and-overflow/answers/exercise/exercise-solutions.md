# Exercise Solution: Operators, Conversions, and Overflow

```c
#include <inttypes.h>
#include <stdint.h>
#include <stdio.h>

int main(void)
{
    const int first = 1200000000;
    const int second = 900000000;
    const int third = 600000000;
    const int64_t total =
        (int64_t)first + (int64_t)second + (int64_t)third;
    const double average = (double)total / 3.0;

    printf("total: %" PRId64 "\n", total);
    printf("average: %.1f\n", average);
    return 0;
}
```

## Why this solution works

The total is 2700000000, the average is 900000000.0, and no overflowing int addition occurs first. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

