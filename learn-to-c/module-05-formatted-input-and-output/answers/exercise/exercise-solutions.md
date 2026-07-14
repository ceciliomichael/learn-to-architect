# Exercise Solution: Formatted Input and Output

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char food[40] = "";

    fputs("Favorite food: ", stdout);
    if (fgets(food, sizeof food, stdin) == NULL) {
        fputs("No food was read.\n", stderr);
        return EXIT_FAILURE;
    }

    printf("You chose: %s", food);
    return EXIT_SUCCESS;
}
```

## Why this solution works

Success and failure take different paths, input is bounded by the array size, and no format warning appears. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

