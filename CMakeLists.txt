cmake_minimum_required(VERSION 2.6)

project(ngfd-plugin-droid-vibrator)

find_package(PkgConfig REQUIRED)
pkg_check_modules(GLIB REQUIRED glib-2.0)
pkg_check_modules(NGFD_PLUGIN REQUIRED ngf-plugin)
pkg_check_modules(ANDROID_HEADERS REQUIRED android-headers)
pkg_check_modules(DROID_VIBRATOR REQUIRED libvibrator)
pkg_check_modules(LIBHARDWARE REQUIRED libhardware)

include_directories(${GLIB_INCLUDE_DIRS})
include_directories(${NGFD_PLUGIN_INCLUDE_DIRS})
include_directories(${ANDROID_HEADERS_INCLUDE_DIRS})
include_directories(${DROID_VIBRATOR_INCLUDE_DIRS})
include_directories(${LIBHARDWARE_INCLUDE_DIRS})

add_library(ngfd_droid-vibrator SHARED src/droid-vibrator.c)

target_link_libraries(ngfd_droid-vibrator ${NGFD_PLUGIN_LIBS})
target_link_libraries(ngfd_droid-vibrator ${DROID_VIBRATOR_LIBS})
target_link_libraries(ngfd_droid-vibrator ${LIBHARDWARE_LIBS})

set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} ${NGFD_PLUGIN_LDFLAGS}")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} ${DROID_VIBRATOR_LDFLAGS}")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} ${LIBHARDWARE_LDFLAGS}")

install(TARGETS ngfd_droid-vibrator LIBRARY DESTINATION lib/ngf)
