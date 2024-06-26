cmake_minimum_required(VERSION 3.10)

# Set the project name
project(FPV_Camera)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add the executable
add_executable(fpv_camera src/fpv_camera.cpp)

# Find GLFW package
find_package(glfw3 3.3 REQUIRED)
if (NOT glfw3_FOUND)
    message(FATAL_ERROR "GLFW not found")
endif()

# Include GLEW
find_package(GLEW REQUIRED)
if (NOT GLEW_FOUND)
    message(FATAL_ERROR "GLEW not found")
endif()

# Include GLM
find_package(glm REQUIRED)
if (NOT glm_FOUND)
    message(FATAL_ERROR "GLM not found")
endif()

# Include directories for GLFW, GLEW, and GLM
include_directories(${GLEW_INCLUDE_DIRS} ${GLFW_INCLUDE_DIRS} ${GLM_INCLUDE_DIRS})

# OpenGL library
find_package(OpenGL REQUIRED)
if (NOT OPENGL_FOUND)
    message(FATAL_ERROR "OpenGL not found")
endif()

# Link against GLEW, GLFW, and OpenGL
target_link_libraries(fpv_camera ${GLEW_LIBRARIES} glfw OpenGL::GL)