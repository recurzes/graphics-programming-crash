cmake_minimum_required(VERSION 3.10)
project(simple_window)

find_package(PkgConfig REQUIRED)
pkg_check_modules(GLEW REQUIRED glew)
pkg_check_modules(GLFW REQUIRED glfw3)
find_package(OpenGL REQUIRED)

add_executable(simple_window simple_window.cpp)

target_include_directories(simple_window PRIVATE
    ${GLEW_INCLUDE_DIRS}
    ${GLFW_INCLUDE_DIRS}
)

target_link_libraries(simple_window
    ${GLEW_LIBRARIES}
    ${GLFW_LIBRARIES}
    OpenGL::GL
)
