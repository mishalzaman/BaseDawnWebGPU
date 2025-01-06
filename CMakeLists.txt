add_executable(App main.cpp)
target_link_libraries(App PRIVATE webgpu)
cmake_minimum_required(VERSION 3.29.0-rc3)
project(
    TestWebGPU
    VERSION 0.1.0 # any version number
    LANGUAGES CXX C # programming languages used by the project
)
set_target_properties(App PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
    COMPILE_WARNING_AS_ERROR ON
)
if (MSVC)
    target_compile_options(App PRIVATE /W4)
else()
    target_compile_options(App PRIVATE -Wall -Wextra -pedantic)
endif()

add_subdirectory(webgpu)

# The application's binary must find wgpu.dll or libwgpu.so at runtime,
# so we automatically copy it (it's called WGPU_RUNTIME_LIB in general)
# next to the binary.
target_copy_webgpu_binaries(App)