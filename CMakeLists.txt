cmake_minimum_required(VERSION 3.10)
project(gtkdemo C)

# Set default build type to Debug if not specified
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug CACHE STRING "Build type (Debug, Release, etc.)" FORCE)
endif()

# Enable debug symbols for Debug builds
set(CMAKE_C_FLAGS_DEBUG "-g")

# Use pkg-config to find GTK4
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK4 REQUIRED gtk4)

# Create the executable
add_executable(gtkdemo main.c)

# Include GTK headers
target_include_directories(gtkdemo PRIVATE ${GTK4_INCLUDE_DIRS})

# Link GTK libraries
target_link_libraries(gtkdemo PRIVATE ${GTK4_LIBRARIES})

# Add any additional compiler flags from pkg-config
target_compile_options(gtkdemo PRIVATE ${GTK4_CFLAGS_OTHER})

# (Optional) Add GTK library paths (usually not needed on Raspberry Pi)
link_directories(${GTK4_LIBRARY_DIRS})

# Optional: Ensure rpath includes GTK library paths (if needed)
set_target_properties(gtkdemo PROPERTIES
  INSTALL_RPATH_USE_LINK_PATH TRUE
  BUILD_RPATH "${GTK4_LIBRARY_DIRS}"
)
