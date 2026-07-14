# Module 28: CMake and Installed Libraries

## What you will learn

This module builds the next production C skill without hiding its contracts.

## C has no standard package manager

Libraries may come from an operating system, a toolchain environment, vcpkg, Conan, or another source. Document how supported platforms obtain the same dependency.

## CMake generates a native build

Set the C standard on each target and disable extensions when ISO portability is intended. Configure into a separate build directory.

## Imported targets carry requirements

A target such as ZLIB::ZLIB supplies include paths, link files, definitions, and transitive requirements. Review dependency upgrades like source changes.

## Complete example

This example requires zlib development files that CMake can discover.

```cmake
cmake_minimum_required(VERSION 3.26)
project(zlib_version LANGUAGES C)

find_package(ZLIB REQUIRED)
add_executable(zlib_version main.c)
target_compile_features(zlib_version PRIVATE c_std_17)
set_target_properties(zlib_version PROPERTIES C_EXTENSIONS OFF)
target_link_libraries(zlib_version PRIVATE ZLIB::ZLIB)
```

```c
#include <stdio.h>
#include <zlib.h>

int main(void)
{
    printf("zlib: %s\n", zlibVersion());
    return 0;
}
```

Build and run:

```text
cmake -S . -B build
cmake --build build
```

Expected result:

```text
The program reports the installed zlib runtime version.
```

## Common mistake

Adding only a header search path does not describe definitions, link files, binary configuration, or transitive requirements.

## Practice and continue

Work through the [exercise](exercise/exercise.md), then the [quiz](quiz/quiz.md). Check the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md) only afterward.

Continue to [Module 29](../module-29-threads-atomics-and-memory-ordering/README.md).
