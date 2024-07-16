cmake_minimum_required(VERSION 3.16)

set(ENGINE_NAME SpaceIsBlueEngine)
set(GIT_SUBMODULE_TARGET GitSubmoduleTarget)

project(${ENGINE_NAME} LANGUAGES CXX VERSION 0.0.1)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED true)

include(FetchContent)

set(BUILD_SHARED_LIBS OFF)
set(SFML_STATIC_LIBRARIES TRUE)

FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 2.6.x)
FetchContent_MakeAvailable(SFML)

file(GLOB_RECURSE SOURCE_FILES
"src/*.cpp"
)

add_library(
    ${ENGINE_NAME}
    STATIC
    ${SOURCE_FILES}
)

target_include_directories(${ENGINE_NAME} PUBLIC "include")

target_link_libraries(
    ${ENGINE_NAME}
    sfml-system
    sfml-window
    sfml-graphics
    sfml-audio
    sfml-main
)

#add_custom_target(
#    ${GIT_SUBMODULE_TARGET}
#    COMMAND git submodule update --remote
#)

#add_dependencies(${ENGINE_NAME} ${GIT_SUBMODULE_TARGET})