# Exercise Solution: Package and Release C Programs

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#ifndef APP_VERSION
#define APP_VERSION "1.0.0"
#endif

int main(int argument_count, char *arguments[])
{
    if (argument_count == 2 &&
        strcmp(arguments[1], "--version") == 0) {
        printf("careful-c %s\n", APP_VERSION);
        return EXIT_SUCCESS;
    }
    if (argument_count == 1) {
        puts("careful-c is ready");
        return EXIT_SUCCESS;
    }
    fprintf(stderr, "Usage: %s [--version]\n", arguments[0]);
    return EXIT_FAILURE;
}
```

## Why it works

The program is identifiable, and a clean recipient can reproduce the documented build from the package alone. The platform, ownership, and failure contracts remain visible.

