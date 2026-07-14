# Module 30: Networking and Platform Boundaries

## What you will learn

This lesson adds one clearly bounded systems skill to the C17 foundation.

## Sockets are not ISO C

POSIX and Windows expose related but different socket types, headers, startup, cleanup, close operations, errors, and link libraries.

## Keep the boundary narrow

Application code should depend on project-owned functions. Platform-specific source files implement those functions without spreading conditional compilation through the rest of the program.

## Received data is untrusted bytes

A receive call may return part of a message and does not promise a terminating zero byte. Protocols need explicit lengths, framing, limits, byte order, timeouts, and security rules.

## Complete example

```c
#include <stdio.h>
#include <stdlib.h>

#if defined(_WIN32)
#define WIN32_LEAN_AND_MEAN
#include <winsock2.h>
static int network_start(void)
{
    WSADATA data;
    return WSAStartup(MAKEWORD(2, 2), &data) == 0;
}
static void network_stop(void) { (void)WSACleanup(); }
#else
static int network_start(void) { return 1; }
static void network_stop(void) { }
#endif

int main(void)
{
    if (network_start() == 0) {
        fputs("Network setup failed.\n", stderr);
        return EXIT_FAILURE;
    }
    puts("Network platform is ready.");
    network_stop();
    return EXIT_SUCCESS;
}
```

Build and run:

```text
Windows GCC: gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -lws2_32 -o main
POSIX: gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
Network platform is ready.
```

## Common mistake

Never pass socket bytes directly to a string function. The received count, not a hoped-for terminator, defines the valid region.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only after trying.

Continue to [Module 31](../module-31-libraries-abi-contracts-and-foreign-interfaces/README.md).

