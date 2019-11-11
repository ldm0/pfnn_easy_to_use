cmake_minimum_required(VERSION 2.6)
project(pfnn)

add_executable(${PROJECT_NAME} src/pfnn.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/dep/include)
target_link_directories(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/dep/lib)

set(EXTERNAL_LIBS
    OpenGL32.lib
    SDL2.lib
    SDL2main.lib
    glew32s.lib
)

target_link_libraries(${PROJECT_NAME} ${EXTERNAL_LIBS})

# Copy all runtime dependencies(SDL2.dll, heightmaps, networks...) to output_directory
add_custom_command(
    TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${PROJECT_SOURCE_DIR}/assets/
        $<TARGET_FILE_DIR:${PROJECT_NAME}>
)