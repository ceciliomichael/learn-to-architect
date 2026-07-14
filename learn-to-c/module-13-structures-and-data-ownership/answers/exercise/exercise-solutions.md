# Exercise Solution: Structures and Data Ownership

```c
#include <stdio.h>

struct Rectangle {
    double width;
    double height;
};

static double area(const struct Rectangle *rectangle)
{
    if (rectangle == NULL) {
        return 0.0;
    }
    return rectangle->width * rectangle->height;
}

int main(void)
{
    const struct Rectangle rectangle = {
        .width = 8.0,
        .height = 5.5
    };

    printf("%.1f\n", area(&rectangle));
    return 0;
}
```

## Why this solution works

The fields form one value, the function does not modify it, null is handled as documented, and the area is 44.0. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

