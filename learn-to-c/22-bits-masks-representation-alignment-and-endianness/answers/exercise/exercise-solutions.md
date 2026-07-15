# Exercise Solution: Bits, Masks, Representation, Alignment, and Endianness

```c
#include <inttypes.h>
#include <stdalign.h>
#include <stdint.h>
#include <stdio.h>

int main(void)
{
    uint32_t mask =
        (UINT32_C(1) << 1) | (UINT32_C(1) << 5);
    printf("before: 0x%08" PRIx32 "\n", mask);

    mask &= ~(UINT32_C(1) << 1);
    printf("after:  0x%08" PRIx32 "\n", mask);
    printf("bit 5 set: %s\n",
           (mask & (UINT32_C(1) << 5)) != 0U ? "yes" : "no");
    printf("size: %zu, alignment: %zu\n",
           sizeof(uint32_t), alignof(uint32_t));
    return 0;
}
```

## Why this solution works

The original mask is 0x00000022, the final mask is 0x00000020, and bit 5 remains set. The code also keeps the lesson's types, boundaries, ownership, and failure paths visible instead of depending on an unstated assumption.

Compile it with the lesson command and compare actual output with the success check. A different solution is valid when it satisfies every stated contract without warnings.

