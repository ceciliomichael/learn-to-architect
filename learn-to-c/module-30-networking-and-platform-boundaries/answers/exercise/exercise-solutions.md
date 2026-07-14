# Exercise Solution: Networking and Platform Boundaries

```c
/* network.h */
#ifndef NETWORK_H
#define NETWORK_H
int network_start(void);
void network_stop(void);
#endif
```

```c
/* network_posix.c */
#include "network.h"
int network_start(void) { return 1; }
void network_stop(void) { }
```

```c
/* main.c */
#include "network.h"
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    if (network_start() == 0) {
        return EXIT_FAILURE;
    }
    puts("Network platform is ready.");
    network_stop();
    return EXIT_SUCCESS;
}
```

## Why it works

Application code uses one interface, the build selects one implementation, and platform headers stay inside the platform layer. The platform, ownership, and failure contracts remain visible.

