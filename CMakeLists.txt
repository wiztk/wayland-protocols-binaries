cmake_minimum_required(VERSION 3.1)

project(wayland-protocols-binaries)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake/modules/")

find_package(Wayland REQUIRED)
if (WAYLAND_FOUND)
    include_directories(${WAYLAND_CLIENT_INCLUDE_DIR} ${WAYLAND_EGL_INCLUDE_DIR})
    set(LIBS ${LIBS} ${WAYLAND_CLIENT_LIBRARIES} ${WAYLAND_EGL_LIBRARIES})
endif ()

set(WAYLAND_PROTOCOLS_SOURCE_DIR ${PROJECT_SOURCE_DIR}/third_party/wayland-protocols)
set(WAYLAND_SCANNER wayland-scanner)

add_subdirectory(unstable)
