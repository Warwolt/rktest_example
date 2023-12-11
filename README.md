# RK Test Example Repository

This repository contains examples for how to integrate the [RK Test](https://github.com/Warwolt/rktest)
unit test library into a C project.

## CMake and Git Submodule

One straight forward way to include RK Test into your project is to include it
in your source directory as a git submodule, and then include it as a
subdirectory in your `CMakeLists.txt`.

This uses a project structure like the following:

```
├── CMakeLists.txt
├── src
│   ├── main.c
│   ├── factorial.c
│   └── factorial.h
├── tests
|   └── factorial_tests.c
└── external
    └── rktest
        ├── CMakeLists.txt
        ├── include
        │   └── rktest
        │       └── rktest.h
        └── src
            └── rktest.c
```

Assuming we're in the project root, we can add RK Test as a git submodule with:

```
mkdir external
git submodule add https://github.com/Warwolt/rktest.git external/rktest
```

Afterwards, we can add the rktest directory to the projects `CMakeLists.txt`
file, and add a test runner executable that links to `rktest_main`.

```cmake
cmake_minimum_required(VERSION 3.16.0)
project(rktest_cmake_example)
enable_language(C)

# Inlucde RK Test
add_subdirectory(external/rktest)

# Main program
add_executable(${PROJECT_NAME}
    src/main.c
    src/factorial.c
)

# Unit tests
add_executable(tests
    src/factorial.c
    tests/factorial_tests.c
)
target_include_directories(tests PRIVATE src)
target_link_libraries(tests PRIVATE rktest_main)
```
