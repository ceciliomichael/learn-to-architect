# Module 11: Pointers, Addresses, and Null

## What you will learn

You will use a pointer as a typed reference to an existing object, check null before dereferencing, and keep object lifetime visible.

## A pointer stores an address

The address operator & obtains an object's address. A pointer type describes the kind of object expected there. The dereference operator * accesses that pointed-to object.

## Null means no object

A null pointer is a distinguished pointer value that points to no object. Compare with NULL before dereferencing when null is permitted by the function or data contract.

## Lifetime still controls access

A non-null address is not automatically valid. The pointed-to object must still exist, the pointer must be correctly aligned for its type, and the access must obey that object's bounds.

## Complete example

```c
#include <stdio.h>

static void add_bonus(int *score)
{
    if (score != NULL) {
        *score += 5;
    }
}

int main(void)
{
    int score = 80;
    int *location = &score;

    add_bonus(location);
    printf("score: %d\n", score);
    add_bonus(NULL);
    return 0;
}
```

Build and run:

```text
gcc -std=c17 -Wall -Wextra -Wpedantic -Wconversion -Wshadow main.c -o main
```

Expected result:

```text
score: 85
```

## Common mistake

Do not return the address of an automatic local variable. That object stops existing when its function returns, leaving a dangling pointer.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then take the [quiz](quiz/quiz.md). Check your work only after attempting it: [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 12](../12-arrays-pointer-arithmetic-and-bounds/README.md).

