cmake_minimum_required(VERSION 3.22)
project(OpenGLPlayground)
set(CMAKE_CXX_STANDARD 14)

find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

set(GLFW_BUILD_DOCS off CACHE BOOL "GLFW lib only")
set(GLFW_INSTALL off CACHE BOOL "GLFW lib only")

add_subdirectory(./dependence/glfw)

if( MSVC )
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /ENTRY:mainCRTStartup")
endif()

add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME} ${OPENGL_LIBRARIES} glfw)

if( MSVC )
    set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})
endif()