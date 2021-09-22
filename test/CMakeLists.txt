include(GoogleTest)

add_executable(UnitTest
  main.cpp
)

target_include_directories(UnitTest PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}
)

target_link_libraries(UnitTest PRIVATE
  project_warnings
  project_options
  GTest::gtest
	cpp-boilerplate
)

gtest_discover_tests(UnitTest)
