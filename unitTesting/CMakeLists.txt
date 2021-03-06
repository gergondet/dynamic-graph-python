# 
#  Copyright 
# 

INCLUDE(CTest)

set(Python_ADDITIONAL_VERSIONS 2.7 2.6 2.5 2.4 2.3 2.2 2.1 2.0)
INCLUDE(../cmake/python.cmake)
FINDPYTHON()
INCLUDE_DIRECTORIES(${PYTHON_INCLUDE_PATH})

INCLUDE_DIRECTORIES(${Boost_INCLUDE_DIRS})
LINK_DIRECTORIES(${Boost_LIBRARY_DIRS} ${PYTHON_LIBRARY_DIRS})


ADD_DEFINITIONS(-DDEBUG=2)

# provide path to library libdynamic-graph.so
LINK_DIRECTORIES(${DYNAMIC_GRAPH_LIBRARY_DIRS})

INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include)
LINK_DIRECTORIES(${${PROJECT_NAME}_BINARY_DIR}/src)

# Add dynamic-graph compilation flags and link to library libdynamic-graph.so
ADD_DEFINITIONS(${DYNAMIC_GRAPH_CFLAGS})


SET(EXECUTABLE_NAME interpreter-test)

ADD_EXECUTABLE(${EXECUTABLE_NAME} interpreter-test.cc)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} dynamic-graph-python)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} ${DYNAMIC_GRAPH_LIBRARIES} -lpthread -ldl  -lutil)

ADD_TEST(${EXECUTABLE_NAME}  ${EXECUTABLE_NAME})

