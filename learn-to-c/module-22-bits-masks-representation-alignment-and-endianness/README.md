# Module 22: Bits, Masks, Representation, Alignment, and Endianness

## What you will learn

You will manipulate unsigned bits while separating numeric value from its byte representation.

## Use unsigned types for bit operations

Unsigned arithmetic has defined modulo behavior. Masks can select, set, clear, or toggle bits. A shift count must be nonnegative and less than the width of the promoted left operand.

## Objects have size and alignment

sizeof reports storage in bytes, and _Alignof reports an alignment requirement. Padding may exist inside and after structures, so field sizes do not necessarily add to the structure size.

## Endianness describes byte order

Multi-byte integer objects can be stored with the least or most significant byte first. Use memcpy to inspect representation without breaking aliasing rules, and use explicit serialization rules for stored or transmitted data.

## Complete example

```c
#include <inttypes.h>
#include <stdalign.h>
#include <stdint.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    uint32_t flags = UINT32_C(0);
    flags |= UINT32_C(1) << 3;
    printf("flags: 0x%08" PRIx32 "\n", flags);

    const uint32_t value = UINT32_C(1);
    unsigned char bytes[sizeof value] = {0};
    memcpy(bytes, &value, sizeof bytes);

    printf("first byte: %u\n", (unsigned)bytes[0]);
    printf("uint32_t alignment: %zu\n", alignof(uint32_t));
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
The mask is 0x00000008. The first byte and alignment are implementation properties.
```

## Common mistake

Do not infer a portable file or network format by writing a structure's raw bytes. Padding, byte order, widths, and representation can vary.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 23](../module-23-undefined-unspecified-and-implementation-defined-behavior/README.md).

