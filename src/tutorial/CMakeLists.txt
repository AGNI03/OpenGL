file(GLOB_RECURSE SRC_FILES
    *.cpp
)

add_library(tutorial STATIC ${SRC_FILES})

target_include_directories(tutorial PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/..
)

target_link_libraries(tutorial PUBLIC
    OpenGL::GL
    glfw
    glad::glad
    glm::glm
)