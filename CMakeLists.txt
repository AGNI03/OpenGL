cmake_minimum_required(VERSION 3.22)

project(OpenGL LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# ==================== Find Dependencies ====================
find_package(OpenGL REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)

# ==================== Add Subdirectories ====================
add_subdirectory(src)

# ==================== Main Executable ====================
add_executable(${PROJECT_NAME}
    main.cpp                    # If main.cpp is in root
    # Or better: src/main.cpp
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    OpenGL::GL
    glfw
    glad::glad
    glm::glm
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    tutorial
    exercise
)

# ==================== Compile Options ====================
if (MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE
        /W4
        /external:anglebrackets
        /external:W0
        /MP                     # Multi-processor compilation
    )
elseif (CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
    target_compile_options(${PROJECT_NAME} PRIVATE
        -Wall
        -Wextra
        -Wpedantic
    )
endif()