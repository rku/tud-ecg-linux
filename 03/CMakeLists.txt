
cmake_minimum_required(VERSION 2.6)

project(GRAPH_PROG)

# add target to build zip file
set(ZIPFILE "${GRAPH_PROG_BINARY_DIR}/übung3_lab.zip")
set(ZIPCMD  git ls-tree -r HEAD | cut -f 2 | zip -@ '${ZIPFILE}')

message(STATUS ${ZIPCMD})
add_custom_target(zip
    /bin/sh -c '${ZIPCMD}'
    WORKING_DIRECTORY ${GRAPH_PROG_SOURCE_DIR})
set_directory_properties(PROPERTIES
    ADDITIONAL_MAKE_CLEAN_FILES ${ZIPFILE})

# put binary in build root
set(EXECUTABLE_OUTPUT_PATH ${GRAPH_PROG_BINARY_DIR})

include_directories(${GRAPH_PROG_SOURCE_DIR}/include
    ${GRAPH_PROG_SOURCE_DIR}/dependencies/freeglut/include
    ${GRAPH_PROG_SOURCE_DIR}/dependencies/qdbmp/include)

set(CMAKE_CXX_FLAGS "-Wall -O2")

add_executable(graph_prog
    src/main.cpp
    src/application.cpp
    src/abstract_scene.cpp
    src/example_3d_primitives.cpp
    src/example_cons_primitives.cpp
    src/recursive_cubes.cpp
    src/cube_system.cpp
    src/example_primitives.cpp
    src/terrain.cpp
    src/cube_system_split.cpp
    src/example_trans_order.cpp
    dependencies/qdbmp/src/qdbmp.cpp)

target_link_libraries(graph_prog GL GLU glut)

