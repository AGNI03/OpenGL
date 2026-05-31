cmake_minimum_required(VERSION 3.22)

project(ProjectName LANGUAGES CXX) # Replace "ProjectName" with your actual project name

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# ==================== Find Dependencies ====================
find_package(PackageName1 REQUIRED) # Replace "PackageName1" with actual package names, e.g., OpenGL, GLFW, GLAD, GLM
find_package(PackageName2 REQUIRED) # Add as many find_package calls as needed

# ==================== Add Subdirectories ====================
add_subdirectory(src) # Assuming your source files are in a "src" directory. Adjust as necessary.

# ==================== Main Executable ====================
add_executable(${PROJECT_NAME}
    main.cpp
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    library1::library1 # Replace "library::library" with the actual target names from your dependencies
    library2::library2 # Add as many libraries as needed
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