cmake_minimum_required(VERSION 3.11)
cmake_policy(SET CMP0072 NEW)
project(OpenGL_Chapters LANGUAGES CXX)

find_package(PkgConfig REQUIRED)
pkg_check_modules(GLEW REQUIRED IMPORTED_TARGET glew)
pkg_check_modules(GLFW REQUIRED IMPORTED_TARGET glfw3)
find_package(OpenGL REQUIRED)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)



set(EXAMPLE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/chapters")
file(GLOB children RELATIVE "${EXAMPLE_DIR}" "${EXAMPLE_DIR}/*")

foreach (child IN LISTS children) 
    if (IS_DIRECTORY "${EXAMPLE_DIR}/${child}")
        set(src "${EXAMPLE_DIR}/${child}/${child}.cpp")
        if (EXISTS "${src}")
            add_executable(${child} "${src}")
            target_include_directories(${child} PRIVATE "${EXAMPLE_DIR}/${child}")
            
            target_include_directories(${child} PRIVATE
                ${GLEW_INCLUDE_DIRS}
                ${GLFW_INCLUDE_DIRS}
            )

            target_link_libraries(${child} PRIVATE
                PkgConfig::GLEW
                PkgConfig::GLFW
                OpenGL::GL
            )
            message(STATUS "Configured example: ${child}")
        else()
            message(WARNING "Skipping ${child}: source file not found (${src})")
        endif()
    endif()
endforeach()
