cmake_minimum_required(VERSION 3.22)
project(OS_test C)

set(CMAKE_C_STANDARD 11)

add_custom_target(build_loader
        COMMAND nasm ${PROJECT_SOURCE_DIR}/loader.asm -f bin -o ${CMAKE_BINARY_DIR}/main.bin
        COMMAND cp ${CMAKE_BINARY_DIR}/main.bin ${CMAKE_BINARY_DIR}/main.img
        COMMAND truncate -s 1440k ${CMAKE_BINARY_DIR}/main.img
)

add_executable(OS_test main.c)

add_dependencies(OS_test build_loader)