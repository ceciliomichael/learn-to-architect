# Exercise Solution: Multi-File Programs, Storage Duration, and Linkage

```c
/* convert.h */
#ifndef CONVERT_H
#define CONVERT_H

int minutes_to_seconds(int minutes);

#endif
```

```c
/* convert.c */
#include "convert.h"

int minutes_to_seconds(int minutes)
{
    return minutes * 60;
}
```

```c
/* main.c */
#include "convert.h"
#include <stdio.h>

int main(void)
{
    printf("%d\n", minutes_to_seconds(3));
    return 0;
}
```

## Why this solution works

Both translation units use one shared declaration, exactly one definition is linked, and the program prints 180. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

