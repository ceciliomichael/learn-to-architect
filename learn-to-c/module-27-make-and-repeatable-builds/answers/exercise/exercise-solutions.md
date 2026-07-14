# Exercise Solution: Make and Repeatable Builds

```makefile
CC = gcc
CFLAGS = -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow

app: main.o message.o
	$(CC) $(LDFLAGS) main.o message.o $(LDLIBS) -o app

main.o: main.c message.h
message.o: message.c message.h

.PHONY: clean
clean:
	$(RM) app main.o message.o
```

## Why it works

One command uses the declared flags, an unchanged second build compiles nothing, and clean removes only generated files. The relevant inputs, boundaries, and failures remain visible.

