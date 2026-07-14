# Exercise Solution: Undefined, Unspecified, and Implementation-Defined Behavior

```c
#include <limits.h>
#include <stdio.h>

int main(void)
{
    const unsigned width = (unsigned)(sizeof(unsigned) * CHAR_BIT);
    const unsigned highest_bit = 1U << (width - 1U);

    printf("CHAR_BIT: %d\n", CHAR_BIT);
    printf("CHAR_MIN: %d\n", CHAR_MIN);
    printf("CHAR_MAX: %d\n", CHAR_MAX);
    printf("unsigned width: %u\n", width);
    printf("highest unsigned bit: %u\n", highest_bit);
    return 0;
}
```

## Why this solution works

Every reported property comes from the implementation, and the only shift count used is strictly less than the unsigned width. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

