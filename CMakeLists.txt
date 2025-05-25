cmake_minimum_required(VERSION 3.10)
project(gtkdemo C)

# Find GTK 4 via pkg-config
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK4 REQUIRED gtk4)

# Add executable
add_executable(gtkdemo main.c)

# Include GTK headers
target_include_directories(gtkdemo PRIVATE ${GTK4_INCLUDE_DIRS})
target_link_libraries(gtkdemo PRIVATE ${GTK4_LIBRARIES})

# Define necessary macros
target_compile_options(gtkdemo PRIVATE ${GTK4_CFLAGS_OTHER})
