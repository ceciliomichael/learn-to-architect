# Module 27: Make and Repeatable Builds

## What you will learn

This module builds the next production C skill without hiding its contracts.

## A target depends on prerequisites

A Make rule names a target, prerequisites, and a tab-indented recipe. Make rebuilds a missing target or one older than its prerequisites.

## Flags have conventional homes

CPPFLAGS carries preprocessor settings, CFLAGS carries C compiler settings, and LDFLAGS plus LDLIBS carry link settings.

## Cleanup removes generated files

A phony clean target removes objects and executables, never source. The default target should produce the useful program.

## Complete example

Use main.c, message.c, and message.h from a small two-file program, then add:

```makefile
CC = gcc
CPPFLAGS =
CFLAGS = -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow

app: main.o message.o
	$(CC) $(LDFLAGS) main.o message.o $(LDLIBS) -o app

main.o: main.c message.h
message.o: message.c message.h

.PHONY: clean
clean:
	$(RM) app main.o message.o
```

```c
/* message.h */
#ifndef MESSAGE_H
#define MESSAGE_H
void print_message(void);
#endif
```

```c
/* message.c */
#include "message.h"
#include <stdio.h>
void print_message(void) { puts("built by Make"); }
```

```c
/* main.c */
#include "message.h"
int main(void) { print_message(); return 0; }
```

Build and run:

```text
make
./app
```

Expected result:

```text
built by Make
```

## Common mistake

A traditional Make recipe starts with a tab. Spaces that look aligned can still produce a missing-separator error.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only afterward.

Continue to [Module 28](../28-cmake-and-installed-libraries/README.md).

