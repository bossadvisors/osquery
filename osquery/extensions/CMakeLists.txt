# Generate the thrift intermediate/interface code.
add_custom_command(
  COMMAND
    ${THRIFT_COMPILER} --gen cpp:dense "${CMAKE_SOURCE_DIR}/osquery.thrift"
  DEPENDS "${CMAKE_SOURCE_DIR}/osquery.thrift"
  WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/generated"
  OUTPUT ${OSQUERY_THRIFT_GENERATED_FILES} 
)

ADD_OSQUERY_LIBRARY(TRUE osquery_extensions
  ${OSQUERY_THRIFT_GENERATED_FILES}
  extensions.cpp
)

ADD_OSQUERY_TEST(TRUE extensions_test extensions_tests.cpp)
