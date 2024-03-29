cmake_minimum_required ( VERSION ${CMAKE_MINIMUM_REQUIRED_VERSION} )
get_filename_component ( CURRENT_FILE ${CMAKE_CURRENT_LIST_FILE} PATH )
get_filename_component ( CURRENT_FOLDER ${CURRENT_FILE} NAME )
project ( ${CURRENT_FOLDER} )
message ( STATUS "CURRENT_FOLDER = ${CURRENT_FOLDER}" )

include_directories ( ${CMAKE_CURRENT_SOURCE_DIR}/include )

if ( ${LIB_GTEST_FOUND} )
  include_directories ( ${LIB_GTEST_INCLUDEDIR} )
  link_directories ( ${LIB_GTEST_LIBDIR} )
  link_libraries ( ${LIB_GTEST_LIBRARIES} )
endif ()

file ( GLOB_RECURSE INC_FILES LIST_DIRECTORIES FALSE ${CMAKE_CURRENT_SOURCE_DIR}/include/test_*.h* )
file ( GLOB_RECURSE SRC_FILES LIST_DIRECTORIES FALSE ${CMAKE_CURRENT_SOURCE_DIR}/sources/test_*.c* )

add_executable ( ${CURRENT_FOLDER} EXCLUDE_FROM_ALL
  ${CMAKE_CURRENT_SOURCE_DIR}/sources/main.cpp
  ${INC_FILES}
  ${SRC_FILES} )
target_link_libraries ( ${CURRENT_FOLDER} PRIVATE module_add )
add_dependencies ( ${CURRENT_FOLDER} module_add )