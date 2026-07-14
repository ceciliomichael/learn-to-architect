# Exercise Solution: Portability, Standards, and C23

```c
#include <limits.h>
#include <stdio.h>

int main(void)
{
#if defined(__STDC_VERSION__)
    printf("standard value: %ld\n", __STDC_VERSION__);
#else
    puts("standard value unavailable");
#endif
    printf("bits per byte: %d\n", CHAR_BIT);
#if defined(__STDC_VERSION__) && __STDC_VERSION__ >= 202311L
    puts("selected family: C23 or later");
#else
    puts("selected family: before C23");
#endif
    return 0;
}
```

## Why it works

The command selects the language edition, while implementation properties are identified separately. The platform, ownership, and failure contracts remain visible.

