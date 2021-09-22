# Kinect wrapper lib

add_library(cpp-boilerplate
  cpp-boilerplate.cpp
)

target_include_directories(cpp-boilerplate PUBLIC
 ${CMAKE_CURRENT_LIST_DIR}
)

set_target_properties(cpp-boilerplate
  PROPERTIES
  LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib
)

target_link_libraries(cpp-boilerplate PUBLIC
  project_warnings
  project_options
)

# Test drivers

add_executable(cpp-boilerplate-cli
  main.cpp
)

set_target_properties(cpp-boilerplate-cli
  PROPERTIES
  OUTPUT_NAME "cpp-boilerplate"
  RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin
)

target_link_libraries(cpp-boilerplate-cli PRIVATE
  project_warnings
  project_options
  cpp-boilerplate 
)
