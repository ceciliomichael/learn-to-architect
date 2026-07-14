# Exercise Solution: CMake and Installed Libraries

```cmake
cmake_minimum_required(VERSION 3.26)
project(dependency_check LANGUAGES C)
find_package(ZLIB REQUIRED)
message(STATUS "Using zlib ${ZLIB_VERSION}")
add_executable(dependency_check main.c)
target_compile_features(dependency_check PRIVATE c_std_17)
set_target_properties(dependency_check PROPERTIES C_EXTENSIONS OFF)
target_link_libraries(dependency_check PRIVATE ZLIB::ZLIB)
```

```c
#include <stdio.h>
#include <zlib.h>
int main(void)
{
    printf("compiled: %s\n", ZLIB_VERSION);
    printf("runtime: %s\n", zlibVersion());
    return 0;
}
```

## Why it works

Configuration fails clearly when zlib is absent, otherwise the imported target supplies requirements and both versions are reported. The relevant inputs, boundaries, and failures remain visible.
