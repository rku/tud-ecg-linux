
cmake_minimum_required(VERSION 2.6)

project(RASTER_GRAPHICS)

# add target to build zip file
set(ZIPFILE "${RASTER_GRAPHICS_BINARY_DIR}/übung2_lab.zip")
set(ZIPCMD  git ls-tree -r HEAD | cut -f 2 | zip -@ '${ZIPFILE}')

message(STATUS ${ZIPCMD})
add_custom_target(zip
    /bin/sh -c '${ZIPCMD}'
    WORKING_DIRECTORY ${RASTER_GRAPHICS_SOURCE_DIR})
set_directory_properties(PROPERTIES
    ADDITIONAL_MAKE_CLEAN_FILES ${ZIPFILE})

# put binary in build root
set(EXECUTABLE_OUTPUT_PATH ${RASTER_GRAPHICS_BINARY_DIR})

include_directories(${RASTER_GRAPHICS_SOURCE_DIR}/include
                    ${RASTER_GRAPHICS_SOURCE_DIR}/dependencies/freeglut/include)

set(CMAKE_CXX_FLAGS "-Wall -O2")

add_executable(raster_graphics
    src/main.cpp
    src/application.cpp
    src/abstract_tool.cpp
    src/bresenham_circle_tool.cpp
    src/bresenham_line_tool.cpp
    src/canvas_renderer.cpp
    src/canvas_store.cpp
    src/dda_line_tool.cpp
    src/line_fill_tool.cpp
    src/non_recursive_fill_tool.cpp
    src/pen_tool.cpp
    src/preview_renderer.cpp
    src/rectangle_tool.cpp 
    src/recursive_fill_tool.cpp)

target_link_libraries(raster_graphics GL GLU glut)

