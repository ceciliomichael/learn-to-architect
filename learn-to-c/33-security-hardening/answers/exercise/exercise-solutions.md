# Exercise Solution: Security Hardening

```c
#include <limits.h>
#include <stdio.h>
#include <string.h>

static int read_complete_line(char buffer[], size_t capacity)
{
    if (buffer == NULL || capacity < 2U ||
        capacity > (size_t)INT_MAX ||
        fgets(buffer, (int)capacity, stdin) == NULL) {
        return 0;
    }
    char *newline = strchr(buffer, '\n');
    if (newline != NULL) {
        *newline = '\0';
        return 1;
    }
    if (feof(stdin) != 0) {
        return 1;
    }
    int character = 0;
    do {
        character = fgetc(stdin);
    } while (character != '\n' && character != EOF);
    buffer[0] = '\0';
    return 0;
}

int main(void)
{
    char command[16] = "";
    if (read_complete_line(command, sizeof command) == 0) {
        return 1;
    }
    if (strcmp(command, "start") == 0) {
        puts("starting");
    } else if (strcmp(command, "stop") == 0) {
        puts("stopping");
    } else {
        return 1;
    }
    return 0;
}
```

## Why it works

Only complete bounded commands are accepted, excess input is drained, and hardening never replaces validation. The platform, ownership, and failure contracts remain visible.

