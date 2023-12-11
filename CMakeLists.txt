cmake_minimum_required(VERSION 3.16.0)
project(rktest_cmake_example)
enable_language(C)

# Inlucde RK Test
add_subdirectory(external/rktest)

# Main program
if(MSVC)
    add_compile_options(/W4 /WX)
else()
    add_compile_options(-Wall -Wextra -Wpedantic -Werror)
endif()

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

