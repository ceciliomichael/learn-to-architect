# Exercise Solution: Preprocessor, Includes, Macros, and Generic Selection

```c
#include <stdio.h>

#define SQUARE(value) ((value) * (value))
#define TYPE_NAME(value) \
    _Generic((value), int: "int", float: "float", default: "other")

int main(void)
{
    const int input = 6;

    printf("square: %d\n", SQUARE(input));
    printf("first type: %s\n", TYPE_NAME(input));
    printf("second type: %s\n", TYPE_NAME(1.0F));
    return 0;
}
```

## Why this solution works

The macro argument has no side effect, expansion is fully parenthesized, the result is 36, and generic selection names both demonstrated types. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

