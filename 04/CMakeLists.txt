
cmake_minimum_required(VERSION 2.6)

project(CURVES)

# add target to build zip file
set(ZIPFILE "${CURVES_BINARY_DIR}/übung4_lab.zip")
set(ZIPCMD  git ls-tree -r HEAD | cut -f 2 | zip -@ '${ZIPFILE}')

message(STATUS ${ZIPCMD})
add_custom_target(zip
    /bin/sh -c '${ZIPCMD}'
    WORKING_DIRECTORY ${CURVES_SOURCE_DIR})
set_directory_properties(PROPERTIES
    ADDITIONAL_MAKE_CLEAN_FILES ${ZIPFILE})

# put binary in build root
set(EXECUTABLE_OUTPUT_PATH ${CURVES_BINARY_DIR})

include_directories(${CURVES_SOURCE_DIR}/include
    ${CURVES_SOURCE_DIR}/dependencies/freeglut/include)

set(CMAKE_CXX_FLAGS "-Wall -O2")

add_executable(curves
    src/main.cpp
    src/application.cpp
    src/abstract_curve.cpp
    src/bspline.cpp
    src/hermite_spline.cpp
    src/control_points_editor.cpp
    src/lagrange_curve.cpp
    src/bezier_curve.cpp
    src/curve_renderer.cpp)

target_link_libraries(curves GL GLU glut)

