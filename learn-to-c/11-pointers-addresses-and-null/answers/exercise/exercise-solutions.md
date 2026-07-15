# Exercise Solution: Pointers, Addresses, and Null

```c
#include <stdio.h>

static void reset(int *value)
{
    if (value != NULL) {
        *value = 0;
    }
}

int main(void)
{
    int answer = 42;
    reset(&answer);
    printf("%d\n", answer);
    reset(NULL);
    return 0;
}
```

## Why this solution works

The caller's object changes to zero, and the null call performs no dereference. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

