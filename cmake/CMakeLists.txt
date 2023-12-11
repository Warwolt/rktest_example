cmake_minimum_required(VERSION 3.16.0)
project(rktest_cmake_example)
enable_language(C)

add_subdirectory(external/rktest)

if(MSVC)
    add_compile_options(/W4 /WX)
else()
    add_compile_options(-Wall -Wextra -Wpedantic -Werror)
endif()

add_executable(${PROJECT_NAME}
    src/main.c
    src/factorial.c
)

add_executable(tests tests/factorial_tests.c)
target_link_libraries(${PROJECT_NAME} PUBLIC ${RKTEST_MAIN})
