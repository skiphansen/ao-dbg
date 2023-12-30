cmake_minimum_required(VERSION 3.5.1)

set(CMAKE_VERBOSE_MAKEFILE ON)

# set project name and language
project(ao-dbg C)
set(CMAKE_BUILD_TYPE "Debug")

# Compilation options
set(CMAKE_C_FLAGS "-std=gnu99 -Wall -MD")

# Sources for this executable
file(GLOB SOURCES "*.c")
file(GLOB LIB_SOURCES "lib/*.c")
add_executable(ao-dbg ${SOURCES} ${LIB_SOURCES})

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBUSB REQUIRED libusb-1.0)
target_link_libraries(ao-dbg "${LIBUSB_LIBRARIES}")


include_directories(. lib PUBLIC ${LIBUSB_INCLUDE_DIRS})

install(TARGETS ao-dbg DESTINATION sbin/)


