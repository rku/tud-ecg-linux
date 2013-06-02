
cmake_minimum_required(VERSION 2.6)

project(TREE_TEST)

# add target to build zip file
set(ZIPFILE "${TREE_TEST_BINARY_DIR}/übung1_lab.zip")
set(ZIPCMD  git ls-tree -r HEAD | cut -f 2 | zip -@ '${ZIPFILE}')

message(STATUS ${ZIPCMD})
add_custom_target(zip
    /bin/sh -c '${ZIPCMD}'
    WORKING_DIRECTORY ${TREE_TEST_SOURCE_DIR})
set_directory_properties(PROPERTIES
    ADDITIONAL_MAKE_CLEAN_FILES ${ZIPFILE})

# put binary in build root
set(EXECUTABLE_OUTPUT_PATH ${TREE_TEST_BINARY_DIR})

include_directories(${TREE_TEST_SOURCE_DIR}/src)

set(CMAKE_CXX_FLAGS "-Wall -O2")

add_executable(tree_test
    src/main.cxx
    src/tree.cxx)
