# Exercise Solution: Enumerations, typedef, and Flags

```c
#include <stdio.h>

enum Mode {
    MODE_READ,
    MODE_EDIT
};

enum Feature {
    FEATURE_SEARCH = 1U << 0,
    FEATURE_EXPORT = 1U << 1
};

int main(void)
{
    const enum Mode mode = MODE_EDIT;
    unsigned features = FEATURE_SEARCH | FEATURE_EXPORT;

    printf("edit mode: %s\n", mode == MODE_EDIT ? "yes" : "no");
    printf("search: %s\n",
           (features & FEATURE_SEARCH) != 0U ? "enabled" : "disabled");
    printf("export: %s\n",
           (features & FEATURE_EXPORT) != 0U ? "enabled" : "disabled");

    features &= ~((unsigned)FEATURE_EXPORT);
    printf("export now: %s\n",
           (features & FEATURE_EXPORT) != 0U ? "enabled" : "disabled");
    return 0;
}
```

## Why this solution works

The choices and flags have separate roles, both flags begin enabled, and only export is removed. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

