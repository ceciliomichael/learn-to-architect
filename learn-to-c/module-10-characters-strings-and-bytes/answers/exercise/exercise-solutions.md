# Exercise Solution: Characters, Strings, and Bytes

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    const char left[] = "red";
    const char right[] = "blue";
    char combined[24] = "";

    const int written =
        snprintf(combined, sizeof combined, "%s + %s", left, right);
    if (written < 0 || (size_t)written >= sizeof combined) {
        fputs("Combined text did not fit.\n", stderr);
        return 1;
    }

    printf("%s\n", combined);
    printf("length: %zu\n", strlen(combined));
    return 0;
}
```

## Why this solution works

The program proves the formatted result fits before treating it as a complete string and reports a length of 10. The code also keeps the lesson's types, boundaries, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

