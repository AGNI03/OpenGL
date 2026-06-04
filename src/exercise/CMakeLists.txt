file(GLOB_RECURSE SRC_FILES
    *.cpp
)

add_library(exercise STATIC ${SRC_FILES})

target_include_directories(exercise PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/..
)

target_link_libraries(exercise PUBLIC
    OpenGL::GL
    glfw
    glad::glad
    glm::glm
)