# Exercise Solution: Libraries, ABI Contracts, and Foreign Interfaces

```c
/* arithmetic_api.h */
#ifndef ARITHMETIC_API_H
#define ARITHMETIC_API_H
#include <stdint.h>
#ifdef __cplusplus
extern "C" {
#endif
int32_t arithmetic_multiply(int32_t left, int32_t right);
#ifdef __cplusplus
}
#endif
#endif
```

```c
/* arithmetic_api.c */
#include "arithmetic_api.h"
int32_t arithmetic_multiply(int32_t left, int32_t right)
{
    return left * right;
}
```

```c
/* client.c */
#include "arithmetic_api.h"
#include <inttypes.h>
#include <stdio.h>
int main(void)
{
    printf("%" PRId32 "\n", arithmetic_multiply(6, 7));
    return 0;
}
```

## Why it works

One header states the interface, one object defines it, the archive links into a separate client, and the documented example prints 42. The platform, ownership, and failure contracts remain visible.

