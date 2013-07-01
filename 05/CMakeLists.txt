
cmake_minimum_required(VERSION 2.6)

project(RAYTRACER)

# add target to build zip file
set(ZIPFILE "${RAYTRACER_BINARY_DIR}/übung5_lab.zip")
set(ZIPCMD  git ls-tree -r HEAD | cut -f 2 | zip -@ '${ZIPFILE}')

message(STATUS ${ZIPCMD})
add_custom_target(zip
    /bin/sh -c '${ZIPCMD}'
    WORKING_DIRECTORY ${RAYTRACER_SOURCE_DIR})
set_directory_properties(PROPERTIES
    ADDITIONAL_MAKE_CLEAN_FILES ${ZIPFILE})

# put binary in build root
set(EXECUTABLE_OUTPUT_PATH ${RAYTRACER_BINARY_DIR})

include_directories(${RAYTRACER_SOURCE_DIR}/include
    ${RAYTRACER_SOURCE_DIR}/dependencies/freeglut/include)

set(CMAKE_CXX_FLAGS "-Wall -O2 -Wno-narrowing -Wno-unknown-pragmas")

add_executable(raytracer
    src/blinn_phong.cpp
    src/cylinder.cpp
    src/kd_tree.cpp
    src/material.cpp
    src/point_light.cpp
    src/raytracer.cpp
    src/spot_light.cpp
    src/box.cpp
    src/directional_light.cpp
    src/light_source.cpp
    src/phong.cpp
    src/primitive.cpp
    src/scene.cpp
    src/transformation_group.cpp
    src/camera.cpp
    src/intersection_info.cpp
    src/main.cpp
    src/plane.cpp
    src/primitive_group.cpp
    src/sphere.cpp
    src/triangle.cpp)

target_link_libraries(raytracer GL GLU glut)

