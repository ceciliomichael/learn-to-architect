# Exercise Solution: Functions, Scope, and Header Declarations

```c
#include <stdio.h>

static int square(int value);

int main(void)
{
    printf("%d\n", square(7));
    printf("%d\n", square(-3));
    return 0;
}

static int square(int value)
{
    return value * value;
}
```

## Why this solution works

The declaration is visible before both calls, the definition matches it exactly, and the output is 49 followed by 9. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

