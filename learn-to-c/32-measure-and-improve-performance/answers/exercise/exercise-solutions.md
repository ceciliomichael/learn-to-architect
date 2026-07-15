# Exercise Solution: Measure and Improve Performance

```c
#include <inttypes.h>
#include <stdint.h>
#include <stdio.h>
#include <time.h>

int main(void)
{
    const uint32_t count = UINT32_C(10000000);
    uint64_t total = UINT64_C(0);
    const clock_t started = clock();
    for (uint32_t value = 0U; value < count; ++value) {
        total += value;
    }
    const clock_t finished = clock();
    if (started == (clock_t)-1 || finished == (clock_t)-1) {
        return 1;
    }
    printf("total: %" PRIu64 "\n", total);
    printf("processor seconds: %.6f\n",
           (double)(finished - started) / (double)CLOCKS_PER_SEC);
    return 0;
}
```

## Why it works

The result remains observable at 49999995000000, environment and flags are recorded, and timings are treated as noisy observations. The platform, ownership, and failure contracts remain visible.

