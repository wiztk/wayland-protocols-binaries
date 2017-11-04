cmake_minimum_required(VERSION 3.1)

project(wayland-protocols-binaries VERSION 1.11)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake/modules/")

find_package(Wayland REQUIRED)
if (WAYLAND_FOUND)
    include_directories(${WAYLAND_CLIENT_INCLUDE_DIR} ${WAYLAND_EGL_INCLUDE_DIR})
    set(LIBS ${LIBS} ${WAYLAND_CLIENT_LIBRARIES} ${WAYLAND_EGL_LIBRARIES})
endif ()

set(WAYLAND_PROTOCOLS_SOURCE_DIR ${PROJECT_SOURCE_DIR}/third_party/wayland-protocols)
set(WAYLAND_SCANNER wayland-scanner)

add_subdirectory(unstable)

set(CPACK_GENERATOR "TGZ")
set(CPACK_PACKAGE_FILE_NAME "${PROJECT_NAME}-${PROJECT_VERSION}-${CMAKE_SYSTEM_PROCESSOR}")

include(CPack)
